# 布局中的滚动失效和默认拉伸
* 使用 Flexbox 或 Grid 布局时，应该在 Flex 容器或 Grid 容器上显式重置 align-items 的默认值 stretch，避免 UI 被拉伸变形；
* 在具备伸缩性的 Flex 项目上显式设置 min-width: 0 ，或在不需要收缩的项目上显式设置 flex-shrink:0 ，避免 UI 被掠夺变形；
* 在设置对齐方式时，应该添加 safe 关键词来避免数据无法全部展示；
* 如果 Flex 容器同时也是一个滚动容器时，我们应该避开使用 justify-content: flex-end ，即使需要向右对齐（或靠底部对齐），应该尽可能地使用 magin-left: auto （或 margin-top）来替代 justify-content: flex-end。
