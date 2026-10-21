【降龙十八掌 · 收款码放置说明】

1. 微信收款码：
   微信 App → 我 → 服务 → 收付款 → 二维码收款 → 保存二维码
   把图片重命名为 wechat-qr.png 放到本目录（d:\git\assets\）

2. 支付宝收款码：
   支付宝 App → 首页 → 收付款 → 二维码收款 → 保存图片
   把图片重命名为 alipay.png 放到本目录

3. 部署：把 index.html 与 assets/ 整个目录一起上传到服务器网站根目录即可。
   示例（nginx）：
     server {
         listen 80;
         server_name xianglongshibazhang.com;
         root /var/www/xianglongshibazhang;
         index index.html;
     }

4. 也可以托管到 GitHub Pages / Cloudflare Pages（免费），绑定自定义域名即可。

注意：收款码属于个人隐私，请勿提交到公开 Git 仓库。
