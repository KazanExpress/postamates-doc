# postamates-doc
# delivery-service

---
## Endpoints:
### HTTP endpoints:
1) Выдать заказ пользователю:

    - По коду и номеру заказа
        ```
        Запрос:
            method: POST
            url: /postamate/issue
            headers:
                * Authorization: token
            body: IssueOrderDto
        ```
        
        ```
        IssueOrderDto:
            {
                "issueCode": 1,
                "orderId": 1
            }
        ```
        ```
        Ошибки:
            * Неправильный код выдачи (статус 400)       
        ```

    - По коду
    
        ```
        Запрос:
            method: POST
            url: /postamate/issue-by-code
            headers:
                * Authorization: token
            body: IssueCodeDto
        ```
        
        ```
        IssueCodeDto:
            {
                "issueCode": 1,
            }
        ```
        
        ```
        Ответ: 
            id заказа
        ```
        
        ```
        Ошибки:
            * Не найден заказ с таким кодом выдачи (статус 404) 
            * Найдено несколько заказов с таким кодом выдачи (статус 400)      
        ```
      
2) Разместить заказ в ячейку:

    ```
    Запрос:
        method: POST
        url: /postamate/place
        headers:
            * Authorization: token
        body: PlaceOrderDto
    ```
    
    ```
    PlaceOrderDto:
        {
            "cellId": 1,
            "orderId": 1
        }
    ```
    
    ```
    Ошибки:
        * Заказ не найден (статус 404) 
        * Ошибка размещения (заказ уже размещен в другую ячейку или ячейка 
        уже занята или заказ не должен быть размещен в этом постамате - статус 400)      
    ```
3) Забрать просроченный заказ:

    ```
    Запрос:
        method: POST
        url: /postamate/check-courier
        headers:
            * Authorization: token
        body: WithdrawDto
    ```
    
    ```
    WithdrawDto:
        {
            "orderId": 1,
            "courierCode": 1
        }
    ```
    ```
    Ошибки:
        * Код не верен (статус 400)    
    ```
    
4) Проверить код курьера и получить список просроченных заказов:

    ```
    Запрос:
        method: POST
        url: /postamate/check-courier
        headers:
            * Authorization: token
        body: CodeDto
    ```
    
    ```
    CodeDto:
        {
            "code": 1
        }
    ```
    
    ```
    Ответ(список просроченных заказов):
        [
            {
                "orderId": 1,
                "cellId": 1
            }
        ]
    ```
    
    ```
    Ошибки:
        * Код не верен (статус 400)    
    ```

5) Получить телефон службы поддержки:

    ```
    Запрос:
        method: GET
        url: /postamate/support-phone
    ```
    
    ```
    Ответ:
        +7 (111) 111-11-11
    ```
