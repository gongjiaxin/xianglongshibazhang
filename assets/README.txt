【降龙十八掌 · 收款码放置说明】

1. 微信收款码：
   微信 App → 我 → 服务 → 收付款 → 二维码收款 → 保存二维码
   把图片重命名为 wechat-qr.jpg 放到本目录（d:\git\github\xianglongshibazhang\assets\）

2. 支付宝收款码：
   支付宝 App → 首页 → 收付款 → 二维码收款 → 保存图片
   把图片重命名为 alipay.jpg 放到本目录

3. USDT 收款码（TRC20）：
   地址：TJSf3PPBvMKEqrCXQeoqGRSqDRsdgSBNuB
   网络：TRC20
   把该地址的二维码图片（钱包 App 内导出或用二维码工具生成）重命名为
   usdt.jpg 放到本目录。页面会同时展示二维码和地址（可一键复制）。

4. 部署：把 index.html 与 assets/ 整个目录一起上传到服务器网站根目录即可。
   示例（nginx，K8s 清单见 ../k8s/deploy.yaml，宿主机反代见 ../k8s/nginx-proxy.conf）：
     server {
         listen 80;
         server_name xianglongshibazhang.com;
         root /var/www/xianglongshibazhang;
         index index.html;
     }

5. 也可以托管到 GitHub Pages / Cloudflare Pages（免费），绑定自定义域名即可。

注意：收款码属于个人隐私，请勿提交到公开 Git 仓库（.gitignore 已拦截 assets 下所有图片）。
