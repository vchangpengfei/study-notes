
1. github 右上角用户图标下拉选 setting
2. 到 Settings/ Developer settings /Personal access tokens 要选择 Generate new token(classic)这个，进去以后记得选各种权限，不然提交可能会没有访问仓库的权限   导航如下图
![RUNOOB 图标](img.png "RUNOOB")

3. 因为只生成一次，刷新后就不见了，复制
4. 按如下格式执行命令
git remote set-url origin  https://<your_token>@github.com/<USERNAME>/<REPO>.git

git remote set-url origin  https://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@github.com/vchangpengfei/study-notes.git

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

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