# Prepaid Event Objects
## Objetos correspondientes a los eventos emitidos por `api-prepaid` y `batch-prepaid`.

## 1. Eventos de cuenta
* __ACCOUNT_CREATED__

    Se gatilla cuando se emite exitosamente una tarjeta en la primera carga del Cliente.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605"
    }
    ```

## 2. Eventos de tarjeta
* __CARD_CREATED__

    Se gatilla cuando se emite exitosamente una tarjeta en la primera carga del Cliente, o para la tarjeta nueva cuando se realiza un cambio de producto.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "card": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "pan": "517608XXXXXX4840",
            "status": "ACTIVE", 
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __CARD_LOCKED__
    
    Se gatilla cuando se bloquea exitosamente una tarjeta mediante el webservice de bloqueo.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "card": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "pan": "517608XXXXXX4840",
            "status": "LOCKED", 
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __CARD_UNLOCKED__
    
    Se gatilla cuando se desbloquea exitosamente una tarjeta mediante el webservice de bloqueo.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "card": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "pan": "517608XXXXXX4840",
            "status": "ACTIVE", 
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __CARD_CLOSED__
    
    Se gatilla para la tarjeta antigua cuando se realiza un cambio de producto.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "card": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "pan": "517608XXXXXX4840",
            "status": "CLOSED", 
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```

## 3. Eventos de transacción (Compras)
* __TRANSACTION_AUTHORIZED__

    Se puede gatillar en los siguientes momentos:

    - __Online__: Cuando API-Prepago recibe la notificación desde Tecnocom al webservice de callback.
    - __Conciliación con Tecnocom__: Si el archivo de Operaciones Diarias cuenta con la Autorización o Movimiento de la compra y no ha sido recibido en línea.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "AUTHORIZED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "SUSCRIPTION",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REVERSED__

    Se puede gatillar en los siguientes momentos:

    - __Online__: Cuando API-Prepago recibe la notificación desde Tecnocom al webservice de callback. __(Por validar)__.
    - __Conciliación con Tecnocom__: Si el archivo de Operaciones Diarias no cuenta con la Autorización o Movimiento de la compra y ésta ha sido recibido y notificada en línea. __(Por validar)__.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REVERSED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "SUSCRIPTION",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REJECTED__

    Se notifica cuando API-Prepago recibe la notificación. __(Por validar)__.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REJECTED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "SUSCRIPTION",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```

## 4. Eventos de transacción (Cash-in Multicaja)
* __TRANSACTION_AUTHORIZED__

    Se gatilla cuando se registra exitosamente la aprobación de Tecnocom de una transacción de cash-in.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "AUTHORIZED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "CASH_IN_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REVERSED__

    Se puede gatillar en los siguientes momentos:

    - __Online__: Cuando API-Prepago recibe la notificación de que debe reversar un cash-in. API-Prepago hará lo posible por eliminar el abono de la cuenta del cliente cuanto antes.
    - __Conciliación con Multicaja__: Cuando API-Prepago se entera por la conciliación de que Multicaja no procesó el cash-in. Esto cambiará el estado de una Transacción de `Autorizado` a `Reversado`. API-Prepago hará lo posible por eliminar el abono de la cuenta del cliente cuanto antes.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REVERSED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "CASH_IN_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REJECTED__

    Se gatilla cuando API-Prepago no puede procesar un cash-in, porque Tecnocom lo rechaza, o porque Tecnocom no responde. En este último caso, API-Prepago hará lo posible por evitar que la carga original se haya procesado.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REJECTED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "CASH_IN_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```

## 5. Eventos de transacción (Cash-out Multicaja)
* __TRANSACTION_AUTHORIZED__

    Se gatilla cuando se registra exitosamente la aprobación de Tecnocom de una transacción de cash-out.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "AUTHORIZED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "CASH_OUT_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REVERSED__

    Se puede gatillar en los siguientes momentos:

    - __Online__: Cuando API-Prepago recibe la notificación de que debe reversar un cash-out. API-Prepago hará lo posible por reintegrar el dinero a la cuenta del cliente cuanto antes. 
    - __Conciliación con Multicaja__: Cuando API-Prepago se entera por la conciliación de que Multicaja no procesó el cash-out. Esto cambiará el estado de una Transacción de `Autorizado` a `Reversado`. API-Prepago hará lo posible por reintegrar el dinero a la cuenta del cliente cuanto antes.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REVERSED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "CASH_OUT_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REJECTED__

    Se gatilla cuando API-Prepago no puede procesar un cash-out, porque Tecnocom lo rechaza, o porque Tecnocom no responde. En este último caso, API-Prepago hará lo posible por evitar que la carga original se haya procesado.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REJECTED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "CASH_IN_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```

## 6. Eventos de transacción (Cash-out diferido Multicaja)
* __TRANSACTION_AUTHORIZED__

    Se gatilla cuando se registra exitosamente la aprobación de Tecnocom de una transacción de cash-out diferido. Esto ocurre en el momento en que el Cliente solicita el retiro.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "AUTHORIZED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "DEFERRED_CASH_OUT_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REVERSED__

    Se puede gatillar en los siguientes momentos:

    - __Online__: Cuando API-Prepago recibe la notificación de que debe reversar el cash-out diferido en línea. API-Prepago hará lo posible por eliminar el cargo de la cuenta del cliente cuanto antes. 
    - __Conciliación con Multicaja__: Cuando el banco de destino no acepta el dinero, el cargo a la tarjeta será reversado automáticamente.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REVERSED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "DEFERRED_CASH_OUT_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_REJECTED__

    Se gatilla cuando API-Prepago no puede procesar un cash-out diferido, porque Tecnocom lo rechaza, o porque Tecnocom no responde. En este último caso, API-Prepago hará lo posible por evitar que la carga original se haya procesado.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "REJECTED",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "DEFERRED_CASH_OUT_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```
* __TRANSACTION_PAID__

    Este evento se gatilla cuando el banco de destino acepte el depósito.

    ```json
    {
        "user_id": "",
        "account_id": "d036377a-761c-4ca9-9eb3-d2ccdec6e605",
        "transaction": {
            "id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "remote_transaction_id": "c2a0e917-742f-4367-a468-5278ccd8ace2",
            "auth_code": "123456",
            "primary_amount": {
                "currency_code": 152,
                "value": "1000"
            },
            "secondary_amount": {
                "currency_code": 840,
                "value": "10.99"
            },
            "fees": [
                {
                    "amount": {
                        "currency_code": 152,
                        "value": "119"
                    },
                    "type": "CL_IVA"
                }
            ],
            "status": "PAID",
            "merchant": {
                "code": "123456789012345",
                "category": 1234,
                "name": "El Comercio"
            },
            "type": "DEFERRED_CASH_OUT_MULTICAJA",
            "country_code": 152,
            "timestamps": {
                "created_at": "2018-01-14T15:27:42.669Z",
                "updated_at": "2018-03-02T10:03:12.123Z"
            }
        }
    }
    ```