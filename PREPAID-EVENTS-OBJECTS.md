# Prepaid Event Objects
## Objetos correspondientes a los eventos emitidos por `api-prepaid` y `batch-prepaid`.

### 1. Eventos de cuenta
* __ACCOUNT_CREATED__

    Se gatilla cuando se emite exitosamente una tarjeta en la primera carga del Cliente.

    ```json
    {
        user_id: '',
        account_id: 'd036377a-761c-4ca9-9eb3-d2ccdec6e605'
    }
    ```
### 2. Eventos de tarjeta
* __CARD_CREATED__

    Se gatilla cuando se emite exitosamente una tarjeta en la primera carga del Cliente, o para la tarjeta nueva cuando se realiza un cambio de producto.

    ```json
    {
        user_id: '',
        account_id: 'd036377a-761c-4ca9-9eb3-d2ccdec6e605',
        card: {
            id: 'c2a0e917-742f-4367-a468-5278ccd8ace2'
            pan: '517608XXXXXX4840'
            status: 'ACTIVE' 
            timestamps:
                created_at: '2018-01-14T15:27:42.669Z'
                updated_at: '2018-03-02T10:03:12.123Z'
        }
    }
    ```
* __CARD_LOCKED__
    
    Se gatilla cuando se bloquea exitosamente una tarjeta mediante el webservice de bloqueo.

    ```json
    {
        user_id: ''
        account_id: 'd036377a-761c-4ca9-9eb3-d2ccdec6e605',
        card: {
            id: 'c2a0e917-742f-4367-a468-5278ccd8ace2'
            pan: '517608XXXXXX4840'
            status: 'LOCKED' 
            timestamps:
                created_at: '2018-01-14T15:27:42.669Z'
                updated_at: '2018-03-02T10:03:12.123Z'
        }
    }
    ```
* __CARD_UNLOCKED__
    
    Se gatilla cuando se desbloquea exitosamente una tarjeta mediante el webservice de bloqueo.

    ```json
    {
        user_id: '',
        account_id: 'd036377a-761c-4ca9-9eb3-d2ccdec6e605',
        card: {
            id: 'c2a0e917-742f-4367-a468-5278ccd8ace2'
            pan: '517608XXXXXX4840'
            status: 'ACTIVE' 
            timestamps:
                created_at: '2018-01-14T15:27:42.669Z'
                updated_at: '2018-03-02T10:03:12.123Z'
        }
    }
    ```
* __CARD_CLOSED__
    
    Se gatilla para la tarjeta antigua cuando se realiza un cambio de producto.

    ```json
    {
        user_id: ''  // Identificador del usuario
        account_id: 'd036377a-761c-4ca9-9eb3-d2ccdec6e605', // ID de la cuenta/contrato
        card: {
            id: 'c2a0e917-742f-4367-a468-5278ccd8ace2'
            pan: '517608XXXXXX4840'
            status: 'CLOSED' 
            timestamps:
                created_at: '2018-01-14T15:27:42.669Z'
                updated_at: '2018-03-02T10:03:12.123Z'
        }
    }
    ```