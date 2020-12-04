---
title: FileFormat_SYM
---

By myst6re.

## Script entity/function names

This is a text file, not present in the PSX version. Each line is 32 characters (space padded) with the last character = \\n. The first lines are the names of the entities, **except the doors**. And after there are the names of the scripts.

Example:

    Director                       # Entity names
    Squall                        
    Eventline1                     
    Director                       # Script names
    Director::default              
    Director::talk                 
    Director::push                 
    Director::dansho1              
    Squall                         
    Squall::default                
    Squall::talk                   
    Squall::push                   
    Squall::shop                   
    Eventline1                     
    Eventline1::default            
    Eventline1::talk               
    Eventline1::push               
    Eventline1::across             
    Eventline1::touch              
    Eventline1::touchOff           
    Eventline1::touchOn            
