---
description: verisetinden arayüzü göstermek
---

# 🪝 Frontend ile verileri almak

## Bu noktadan başla:

`git clone git@github.com:msdsn/Dynamic-Spline.git`

`git checkout a5d0dc893160a8b82d976605809b72592f9b7e3e`

[_kurulumu tamamla_](djangon-spline.md#backend-baslat)

***

## Backend'den bigileri almak:

<mark style="background-color:purple;">ApiConnection.js</mark> isminde bir dosya oluşturup burada backendden bilgileri alıcam.

#### öncelikle axios indirelim

`npm i axios`

#### clasımızı yazalım

{% code title="frontend/src/ApiConnection.js" %}
```javascript
import axios from 'axios';
export default class ApiConnection
{
    constructor(){
        this.get();
    }
    get(){
        axios.get('http://127.0.0.1:8000/api/products/')
        .then(function (response) {
            // handle success
            console.log(response.data);
        })
        .catch(function (error) {
            // handle error
            console.log(error);
        })
        .finally(function () {
            // always executed
        });
    }
}
```
{% endcode %}

#### cors hatası alıyoruz, djangoda bu hatayı çözelim

* `pip install django-cors-headers`
*   ```
    INSTALLED_APPS = [
    ```

    ```python
        ...
        'corsheaders',
        ...
    ]

    ```
*   <pre><code><strong>MIDDLEWARE = [
    </strong></code></pre>

    <pre class="language-python"><code class="lang-python">    ...
        <a data-footnote-ref href="#user-content-fn-1">'corsheaders.middleware.CorsMiddleware',</a>
        'django.middleware.common.CommonMiddleware',
        ...
    ]
    </code></pre>
* `CORS_ALLOW_ALL_ORIGINS = True`
  * not:Tüm kökenlere izin vermek güvenlik açısından önerilmez, sadece test amaçlı kullanılmalıdır aşağıdaki ayarı kullanabilirsiniz:
    *   ```
        CORS_ALLOWED_ORIGINS = [
        ```

        ```python
            'http://localhost:5173',
            'http://127.0.0.1:5173',
        ]
        ```

## Sonuç:

```json
[
    {
        "name": "Ball",
        "brand": "Future",
        "category": "Football",
        "stock": 30
    },
    {
        "name": "Shirt",
        "brand": "Future",
        "category": "3d",
        "stock": 12
    }
]
```

[^1]: `CorsMiddleware`'i ekleyin ve onu `CommonMiddleware`'den hemen önce yerleştirin
