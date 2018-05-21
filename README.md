# マインスイーパー・ミニアプリ

モグラ叩きみたいにミニアプリの実装はチェックポイントに分解されています。

`git checkout checkpoint-0` から初めてください！

# Git のワークフロー

1. [ ] Begin by **forking** this repository.

![forking](https://i.imgur.com/PmLC0ON.png)

2. [ ] Then, clone down your fork: `git clone YOUR_FORK_URL`

3. [ ] Then, checkout the appropriate checkpoint branch. Example, for checkpoint 0:

`git checkout checkpoint-0` (checkpoint-0 is the branch name)

4. [ ] Read `checkpoints/checkpoint-0.md` (for checkpoint 0)

5. [ ] Do some work, then make a commit using `git commit`.

6. [ ] Once you finish the work for a checkpoint, checkout the next branch. Example: `git checkout checkpoint-1`

7. [ ] Continue working until you finish!

## セットアップ

``` bash
# install dependencies
npm install
```

## アプリを実行する

```bash
# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

セットアップに関して詳しくは [VueJS Templates Guide](http://vuejs-templates.github.io/webpack/) と [Vue-Loader Docs](http://vuejs.github.io/vue-loader) をご覧ください。
