# Repository architecture / 仓库结构

```text
catalog.lock.json       selected additions, authors, versions, distribution integrity
catalog/<plugin>/       English + Chinese feature/installation/configuration docs
plugins/                two imported local ESM/React plugins with provenance
licenses/               observed upstream license texts, kept per package
scripts/collection.py   read-only plan → isolated staging → verified fetch → new profile
scripts/inventory.py    metadata-only discovery of non-built-in plugin packages
scripts/check.py        catalog/doc/link/source/secret checks
templates/              reviewed compatibility guards (not personal account config)
tests/                  installer behavior and isolated host-route contracts
```

The catalog separates a package's declared bundle from runtime activation. UI aggregates own seven child packages; the installer selects roots rather than mounting duplicate children. Built-in base/web names are prerequisite references and contain no copied host code.
清单区分包声明与运行时启用；UI 聚合包管理七个子包，安装器选择根项，避免重复注册。base/web 名称只是宿主依赖引用，未复制官方源码。

Third-party roots are fetched from their fixed distribution URLs and checked against recorded SRI values. Their dependencies are then resolved by the chosen package manager with lifecycle scripts disabled. A generated profile receipt records the catalog digest and whether dependency fetch completed. It contains no credentials, but its local paths make it a local artifact rather than a public release file.
第三方根包固定 URL 并校验 SRI，随后由包管理器解析依赖，禁用生命周期脚本。新 Profile 的回执记录清单摘要与安装结果，不含凭据，但带本地路径，不能当作公共发行文件。
