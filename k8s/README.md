# 降龙十八掌 · K8s 部署

## 文件说明
| 文件 | 用途 |
|---|---|
| `deploy.yaml` | Namespace + ConfigMap + Deployment + Service(NodePort) + Ingress 一把梭 |
| `nginx-proxy.conf` | 宿主机 nginx 反代（80 → NodePort 30088，无 443） |

## 流量路径（两条路二选一）
- **走 Ingress**：DNS A 记录 → ingress-nginx 的 LB/节点，host 为 `a.xianglongshibazhang.com`
- **走宿主机 nginx**：DNS A 记录 → 宿主机，nginx 80 → `127.0.0.1:30088` → Service → Pod

## 部署步骤

```bash
# 1. 拷贝静态文件到节点（hostPath 要求每个可能调度的节点都有）
mkdir -p /data/git/test/xianglongshibazhang
cp index.html assets/ /data/git/test/xianglongshibazhang/ -r

# 2. 部署到 k8s
kubectl apply -f deploy.yaml

# 3. 验证
kubectl -n xianglongshibazhang get pod,svc,ingress
curl -H 'Host: a.xianglongshibazhang.com' http://<节点IP>:30088/

# 4.（可选）宿主机 nginx 反代
cp nginx-proxy.conf /etc/nginx/conf.d/a.xianglongshibazhang.conf
nginx -t && nginx -s reload
```

## 注意
- 线上已有 `xianglongshibazhang.com`，K8s 环境统一用 `a.xianglongshibazhang.com` 避免访问冲突（DNS 需为 `a` 加一条 A 记录指向对应 IP）
- 容器端口 / Service 端口均为 **8080**，NodePort **30088**
- hostPath 目录不存在时 Pod 会起不来（`type: Directory`），属预期行为，便于发现文件没拷
- 收款码图片不要进 Git 仓库（根目录 .gitignore 已拦截），直接放到服务器 `/data/git/test/xianglongshibazhang/assets/`
