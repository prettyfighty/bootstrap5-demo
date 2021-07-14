# Install Bootstrap v5 to your Rails Projects

我的[部落格](https://lailai-blog.gq)：https://lailai-blog.gq

詳細步驟與說明，請參考[這篇文章](https://lailai-blog.gq/2021/07/14/Install-Bootstrap-To-Your-Rails-Projects/)


# Steps

1. $ rails new bootstrap5-demo

2. $ cd bootstrap5-demo

3. $ yarn add bootstrap jquery @popperjs/core@^2.9.2

4. 修改 config/webpack/environment.js

```js
// config/webpack/environment.js

const { environment } = require('@rails/webpacker')
const webpack = require('webpack')

environment.plugins.prepend(
  'Provide',
  new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery',
    jquery: 'jquery',
    Popper: ['@popperjs/core'],
  })
)

module.exports = environment
```

5. 在 app/javascript/packs/application.js 引入 bootstrap，並參考官網設定popovers及tooltips

```js
// app/javascript/packs/application.js

import "styles"

// bootstrap
import "bootstrap"
const bootstrap = require('bootstrap')

document.addEventListener("turbolinks:load", () => {
  var tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'))
  var tooltipList = tooltipTriggerList.map(function (tooltipTriggerEl) {
    return new bootstrap.Tooltip(tooltipTriggerEl)
  })
  var popoverTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="popover"]'))
  var popoverList = popoverTriggerList.map(function (popoverTriggerEl) {
    return new bootstrap.Popover(popoverTriggerEl)
  })
})
```

6. 在 app/javascript 目錄下，新增 styles 資料夾，並在該資料夾內新增 index.js 及 bootstrap.scss 檔案

```js
// app/javascript/packs/application.js

import "styles"
```

```scss
// app/javascript/styles/bootstrap.scss

@import '~bootstrap/scss/bootstrap'
```

7. 找到 /app/views/layouts/application.html.erb 檔案，將stylesheet後面的link改成pack

```html
-  <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
+  <%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
```

8. $ rails g controller static home，新增一個名叫 static 的 controller 以及 home 方法

9. 到官網複製一些程式碼，例如NavBar、popovers、tooltips，貼到 app/views/static/home.html.erb

```html
<div class="container">
  <h1>Static#home</h1>
  <p>Find me in app/views/static/home.html.erb</p>

  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
              Dropdown
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
              <li><a class="dropdown-item" href="#">Action</a></li>
              <li><a class="dropdown-item" href="#">Another action</a></li>
              <li><hr class="dropdown-divider"></li>
              <li><a class="dropdown-item" href="#">Something else here</a></li>
            </ul>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li>
        </ul>
        <form class="d-flex">
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
      </div>
    </div>
  </nav>

  <div class="mb-5"></div>

  <button type="button" class="btn btn-lg btn-danger" data-bs-toggle="popover" title="Popover title" data-bs-content="And here's some amazing content. It's very engaging. Right?">Click to toggle popover</button>

  <div class="mb-5"></div>

  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="top" title="Tooltip on top">
    Tooltip on top
  </button>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="right" title="Tooltip on right">
    Tooltip on right
  </button>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="bottom" title="Tooltip on bottom">
    Tooltip on bottom
  </button>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="left" title="Tooltip on left">
    Tooltip on left
  </button>
</div>
```

10. $ bin/webpack-dev-server，開啟 webpacker 打包 css 及 js 檔案

11. 再開啟一個終端機，cd切換到專案的目錄（參考步驟2.，像我就是cd到tailwind_css），並輸入$rails s 開始本地伺服器




