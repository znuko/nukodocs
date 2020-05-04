---
title: Plugins
---

!!! warning
    `plugins` を設定する際、デフォルトでオンになっていた `search` pluginを引き続き使用するなら、それを明記しないといけない；
    ```yaml
    plugins:
      - search # necessary for search to work
      ...
    ```

# Material

## Revision date

記事の下に更新日付を付加する。

- [Revision date - Material for MkDocs](https://squidfunk.github.io/mkdocs-material/plugins/revision-date/)

### Installation

```
pip install mkdocs-git-revision-date-localized-plugin
```

`mkdocs.yml`:

```yaml
plugins:
  - git-revision-date-localized:
      type: date
```

### Format

> default: `type: date`

```
最終更新日: 2020年5月4日             # type: date
最終更新日: 2020年5月4日 02:04:51    # type: datetime
最終更新日: 2020-05-04              # type: iso_date
最終更新日: 2020-05-04 02:06:53     # type: iso_datetime
最終更新日: 9時間前                  # type: timeago
```