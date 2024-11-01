# Maskify - Sensitive Data Masking Library for Python

![PyPI - Version](https://img.shields.io/pypi/v/maskify-py?color=%23ffd43b)
![PyPI - Downloads](https://img.shields.io/pypi/dm/maskify-py?color=%23ffd43b)


**Maskify** is a lightweight, flexible library for Python, inspired by the [Maskify.Core](https://github.com/djesusnet/Maskify.Core) library for .NET. It helps developers securely mask sensitive data, such as Brazilian documents (CPF, CNPJ), emails, credit cards, and phone numbers. This library provides built-in masking for common data types, along with customizable masking options to ensure compliance with data protection regulations.

## Features

- **Mask CPF and CNPJ**: Easily mask Brazilian CPF and CNPJ numbers.
- **Email Masking**: Partially mask email addresses.
- **Credit Card Masking**: Mask credit card numbers while preserving the last few digits.
- **Phone Number Masking**: Support for mobile and residential phone numbers.
- **Custom Masking**: Mask any string by specifying a start position, length, and masking character.

## Installation

To install Maskify, run:

```bash
pip install maskify-py
```

## Usage

Below are examples of using Maskify for different types of sensitive data.

### 1. Masking CPF

The CPF format consists of 11 digits. Maskify will retain the last two digits and mask the middle portion:

```python
from maskify.masker import Masker

cpf = "123.456.789-01"
masked_cpf = Masker.mask_cpf(cpf, "*")
print("Output:", masked_cpf)  

# Output: "123.***.**9-01"
```

### 2. Masking CNPJ

The CNPJ format consists of 14 digits. Maskify will retain the first two and last two digits, masking the middle portion:

```python
from maskify.masker import Masker

cnpj = "12.345.678/0001-99"
masked_cnpj = Masker.mask_cnpj(cnpj, "*")
print("Output:", masked_cnpj)  

# Output: "12.***.***/**01-99"
```

### 3. Masking email

The email masking function hides a portion of the local part of the email (before `@`), leaving the first and last characters visible:

```python
from maskify.masker import Masker

email = "usuario@exemplo.com"
masked_email = Masker.mask_email(email, "*")
print("Output:", masked_email)  

# Output: "u*****o@exemplo.com"
```

### 4. Masking credit card

Maskify supports multiple credit card formats, including standard 16-digit cards, American Express (15 digits), and Diners Club (14 digits). It retains only the last four digits, masking the rest:

```python
from maskify.masker import Masker

credit_card = "1234 1234 1234 1234"
masked_credit_card = Masker.mask_credit_card(credit_card, "*")
print("Output:", masked_credit_card)  

# Output: "**** **** **** 1234"
```

### 5. Masking mobile phone numbers

Mobile phone numbers with 11 digits are masked to display only the area code, first digit, and last four digits:

```python
from maskify.masker import Masker

mobile_phone = "(11) 91234-5678"
masked_mobile_phone = Masker.mask_mobile_phone(mobile_phone)
print("Output:", masked_mobile_phone)  

# Output: "(11) *****-5678"
```

### 6. Masking residential phone numbers

Residential phone numbers with 10 digits are masked to display only the area code, first two digits, and last four digits:

```python
from maskify.masker import Masker

residential_phone = "(11) 1234-5678"
masked_residential_phone = Masker.mask_residential_phone(residential_phone)
print("Output:", masked_residential_phone)  

# Output: "(11) ****-5678"
```

### 7. Custom Masking

Maskify provides a general `mask` function to apply a mask to any string. Specify the start position, length of the mask, and masking character:

```python
from maskify.masker import Masker

text = "Confidential"
masked_text = Masker.mask(text, start_position=2, length=8)
print("Output:", masked_text)  

# Output: "Co********al"
```

## Error Handling

If input values do not meet format requirements, Maskify functions raise a `ValueError` with a descriptive message. Ensure that inputs are in the expected format (e.g., 11 digits for CPF, 14 digits for CNPJ) to avoid exceptions.

## Contributing

We welcome contributions to enhance Maskify! Feel free to submit issues or pull requests. For major changes, please open a discussion first to share your proposed changes.

## License

This project is licensed under the MIT License.
