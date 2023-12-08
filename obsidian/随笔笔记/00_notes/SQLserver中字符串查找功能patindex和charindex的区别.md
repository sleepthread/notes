SQLserver中字符串查找功能patindex和charindex的区别

包括 1、全匹配查找字符串
2、模糊查找字符串 CHARINDEX 和 PATINDEX 函数都返回指定模式的开始位置。PATINDEX 可使用通配符，而 CHARINDEX 不可以。
　　这两个函数都带有2个参数：
　　1 希望获取其位置的模式。使用 PATINDEX，模式是可以包含通配符的字面字符串。使用 CHARINDEX，模式是字面字符串（不能包含通配符）。
　　2 字符串值表达式（通常为列名）。
　　例如，查找模式"wonderful"在 titles 表中 notes 列的某一特定行中的开始位置。