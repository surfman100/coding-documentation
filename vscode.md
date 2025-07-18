# VSCode
Hints & tips on using VSCode

## View in a browser
Add the following tasks.json

                                "version": "2.0.0",
                                "tasks": [
                                        {
                                            "label": "echo",
                                            "type": "shell",
                                            "command": "echo Hello"
                                        },
                                        {
                                            "label": "chrome",
                                            "type": "process",
                                            "command": "chrome.exe",
                                            "windows": {
                                                "command": "C:\\Program Files (x86)\\Google\\Chrome\\Application\\chrome.exe"
                                            },
                                            "args": [
                                                "${file}"
                                            ],
                                            "group": {
                                                "kind": "build",
                                                "isDefault": true
                                            }
                                        }
                                    ]
                                }
