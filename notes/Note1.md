## 设置和代码库理解                                                  2 -1. CLAUDE.md记忆，                                            
       3 -                                                                     4 -    Claude Code 有两套记忆系统：                                     5 -                                                                     6 -    CLAUDE.md 文件 - 由用户编写的持久化指令                          7 -    Auto memory - Claude 自动生成的学习笔记                          8 -    自动记忆 - Claude 自动生成的学习笔记, Auto memory                  -存储在 ~/.claude/projects/<project>/memory/ 目录下                   9 -                                                                    10 -2. 三种类型claude md文件:1: 2: 3:                                   11 -                                                              
      12 -3. VSCode中直接使用Terminal打开Claude Code无法使用/ide 
         -命令连接VSCode，可使用Ctrl + Shift + P-->Claude Code: O       
         -pen in Terminal, 但是无法使用#号自动记录到CLAUDE.md中         
      13 -                                                              
      14 -4. https://code.claude.com/docs/en/memory 对这篇文档进        
         -行总结，然后以三级标题总结写在这里                            
      15 -    >CLAUDE.md files can import additional files using        
         -@path/to/import syntax. Imported files are expanded and       
         - loaded into context at launch alongside the CLAUDE.md        
         -that references them. 使用@path/to/import导入到CLAUDE.m       
         -d的知识在本次会话中使用对吗，而不会真正的添加到CLAUDE.m       
         -d文件中                                                       
      16 -    CLAUDE.md文件可以使用@path/to/import语法导入其他文        
         -件。导入的文件在启动时与引用它们的CLAUDE.md文件一起展开       
         -并加载到上下文中。使用@path/to/import导入到CLAUDE.md的        
         -知识在本会话中使用是正确的，但不会真正添加到CLAUDE.md文       
         -件中。                                                        
      17 -    >                                                         
      18 -    >Read 1 file 读取1个文件                                  
      19 -    是的，你理解正确！                                        
      20 -    >                                                         
      21 -    >使用 @path/to/import 语法导入的文件会在会话启动时        
         -被展开并加载到上下文中，但不会真正修改 CLAUDE.md 文件本       
         -身。                                                          
      22 -    >                                                         
      23 -    >这只是一种引用机制，让你可以把其他文件的内容（如 R       
         -EADME、package.json 等）作为上下文加载，而不需要复制粘        
         -贴到 CLAUDE.md 中。原始的 CLAUDE.md 文件内容保持不变。        
      24 -                                                              
      25 -    将这段引用也跟上面连接中的文档一起总结                    
      26 -                                                              
      27 -5. 可在settings.json中添加  "autoMemoryEnabled": false        
         -来控制自动记忆的开启和关闭，也可以放到项目文件夹中.clau       
         -de/settings.local.json中   