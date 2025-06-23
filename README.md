# 飞书自定义 Bot 的 CI 推送

## 使用

到 [https://open.feishu.cn/cardkit](飞书卡片搭建工具) 搭建如下卡片

```json

{
    "schema": "2.0",
    "config": {
        "update_multi": true,
        "style": {
            "text_size": {
                "normal_v2": {
                    "default": "normal",
                    "pc": "normal",
                    "mobile": "heading"
                }
            }
        }
    },
    "body": {
        "direction": "vertical",
        "horizontal_spacing": "8px",
        "vertical_spacing": "8px",
        "horizontal_align": "left",
        "vertical_align": "top",
        "padding": "12px 12px 12px 12px",
        "elements": [
            {
                "tag": "column_set",
                "flex_mode": "flow",
                "horizontal_spacing": "8px",
                "horizontal_align": "left",
                "columns": [
                    {
                        "tag": "column",
                        "width": "weighted",
                        "elements": [
                            {
                                "tag": "markdown",
                                "content": "**镜像名称**\n${ci_target_image}",
                                "text_align": "left",
                                "text_size": "normal_v2",
                                "margin": "0px 0px 0px 0px"
                            }
                        ],
                        "vertical_spacing": "8px",
                        "horizontal_align": "left",
                        "vertical_align": "top",
                        "weight": 1
                    },
                    {
                        "tag": "column",
                        "width": "weighted",
                        "elements": [
                            {
                                "tag": "markdown",
                                "content": "**版本**\n${ci_target_tag}",
                                "text_align": "left",
                                "text_size": "normal_v2",
                                "margin": "0px 0px 0px 0px"
                            }
                        ],
                        "padding": "0px 0px 0px 0px",
                        "direction": "vertical",
                        "horizontal_spacing": "8px",
                        "vertical_spacing": "8px",
                        "horizontal_align": "left",
                        "vertical_align": "top",
                        "margin": "0px 0px 0px 0px",
                        "weight": 1
                    },
                    {
                        "tag": "column",
                        "width": "weighted",
                        "elements": [
                            {
                                "tag": "markdown",
                                "content": "**用时**\n${ci_takes} 秒\n",
                                "text_align": "left",
                                "text_size": "normal_v2",
                                "margin": "0px 0px 0px 0px"
                            }
                        ],
                        "vertical_spacing": "8px",
                        "horizontal_align": "left",
                        "vertical_align": "top",
                        "weight": 1
                    }
                ],
                "margin": "0px 0px 0px 0px"
            }
        ]
    },
    "header": {
        "title": {
            "tag": "plain_text",
            "content": "CI ${result_status} - ${ci_target}"
        },
        "subtitle": {
            "tag": "plain_text",
            "content": ""
        },
        "template": "${result_theme}",
        "padding": "12px 12px 12px 12px"
    }
}
```

然后可以参考 [https://github.com/colour93/ci-notify-feishu-demo/blob/main/.github/workflows/ci.yml](https://github.com/colour93/ci-notify-feishu-demo/blob/main/.github/workflows/ci.yml) 这里编写 workflow