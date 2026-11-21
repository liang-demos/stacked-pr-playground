# GitHub Stacked PR 练习

先把燕麦拿铁加进菜单，再下一笔燕麦拿铁的订单。把这两个改动拆成两个 PR，就能观察第二个 PR 如何依赖第一个。

在仓库根目录的 `main` 分支开始。如果还没装 `gh stack`，先运行 `gh extension install github/gh-stack`。

```sh
gh stack init menu
echo '燕麦拿铁' >> src/menu.txt
git add src/menu.txt
git commit -m "在菜单中加入燕麦拿铁"

gh stack add order
echo '002 燕麦拿铁 x 1' >> src/orders.txt
git add src/orders.txt
git commit -m "记录燕麦拿铁订单"

gh stack submit --auto
gh stack view
```

`submit --auto` 会推送两个分支并创建两个草稿 PR。在 GitHub 上分别查看两个 PR 的 **Files changed**。`menu` 以 `main` 为目标分支，只改了菜单。`order` 以 `menu` 为目标分支，只多了一笔订单。

想试第三层，可以在 `order` 上运行 `gh stack add pickup`，把 `002 已取餐` 写进 `src/pickups.txt`，提交后再运行 `gh stack submit --auto`。[GitHub 官方快速入门](https://docs.github.com/zh/pull-requests/get-started/stacked-prs-quickstart)
