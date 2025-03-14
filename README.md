## this fork has been changed to support US date formatted paypal CSV exports with %d/%m/%Y format
# Beancount PayPal Importer

`beancount-paypal` provides an Importer for converting CSV exports of PayPal into the beancount format.

## Installation

```sh
pip install git+https://github.com/cosmikwolf/beancount-paypal.git
```

## Usage

### Basic usage

Configure `PaypalImporter` in your importer script, and download your PayPal statements as CSV.

In PayPal you can customize the report fields. If you enable `Transaction Details > Balance`, the
beancount output will be finalized with a `balance` assertion.


```python
from beancount_paypal import PaypalImporter

CONFIG = [
    PaypalImporter(
        'my-paypal-account@gmail.com',
        'Assets:US:PayPal',
        'Assets:US:Checking',
        'Expenses:Financial:Commission',
    )
]
```

### Advanced usage

If you enable additional report fields you can map them into transaction metadata using the
`metadata_map` keyword argument:

```python
from beancount_paypal import PaypalImporter, lang

CONFIG = [
    PaypalImporter(
        'my-paypal-account@gmail.com',
        'Assets:US:PayPal',
        'Assets:US:Checking',
        'Expenses:Financial:Commission',
        language=lang.de(),
        metadata_map={
            "uuid": "Transaktionscode",
            "sender": "Absender E-Mail-Adresse",
            "recipient": "Empfänger E-Mail-Adresse"
        }
    )
]
```
