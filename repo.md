# b570_pre

## Repo简介
这是一个用 C++ 编写的命令行社交网络程序（CPPeers）。它支持从文本文件加载用户与帖子数据，并提供按用户、按话题标签筛选帖子以及统计最热门话题的功能。核心模块包括用户、帖子与话题标签的存储与查询逻辑，入口在 `main.cpp` 里提供交互式菜单。

## 题目Prompt
I'm making a basic social media network in C++, where users can input a text file containing posts, search the posts by user or hashtag, or find the most popular hashtag. Please create a function in 'main.cpp' that allows the user to create a post and add it to the database. The function should prompt the user for their username, then prompt them for their message content. If all inputs are valid, the function should register the user in the database if they are new, and add the post to the database, with a new post ID that is higher than any other post in the database. Add this function as an option in the main menu print statement, and add it as a case in the 'main' function in 'main.cpp'. Additionally, could you add comments to the 'loadFromFile' function in 'Network.cpp' that explain how it differentiates between users and posts? This function takes in a file path, and adds new users and posts to the database accordingly.

## PR链接
待创建
