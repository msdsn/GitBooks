# 🧑‍🚀 Spline hazırlık

## Tam burdan başla:

`git clone git@github.com:msdsn/Dynamic-Spline.git`

`git checkout 4994143cf2c1997f9bbedf8734ed065dce69454d`

[_kurulumu tamamla_](djangon-spline.md#backend-baslat)

***

## Öncelikle spline runtime js incelemesi yapalım:

[https://www.npmjs.com/package/@splinetool/runtime](https://www.npmjs.com/package/@splinetool/runtime)

***

## Spline'da oluşturduğumuz yapıyı console'da görelim

<pre class="language-javascript" data-title="frontend/src/Spline.js"><code class="lang-javascript"><strong>import { Application } from '@splinetool/runtime';
</strong>import Experience from '../Experience';
import ApiConnection from '../../ApiConnection';
export default class Spline
{
    constructor(){
        this.experience = new Experience();
        this.canvas = this.experience.canvas;
        this.url = 'https://prod.spline.design/UbLlcZisgA5GVeUB/scene.splinecode'
        this._Init();
    }
    _Init(){
        this.apiConnection = new ApiConnection();
        this.instance = new Application(this.canvas);
        this.instance.load(this.url).then(() => {
            console.log(this.instance)
        });
    }
    update(){
        
    }
}
</code></pre>
