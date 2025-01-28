---
title: Source
---

Source Code Forensics

The PC port's executable contains some very interesting artifacts from it's development cycle. This is a listing of the known source files referenced within Final Fantasy 7's PC executable. This listing is attainable with a single UNIX like command, and cleaned up with a little editing.

strings ff7.exe \| grep '\[cC\]:\\' \| tr '\[:upper:\]' '\[:lower:\]' \| sort \| uniq \> filelist.txt

This is by far not a complete listing of source files. These only reference files that did memory allocation. Their function originally was to trace memory allocations and what source file was responsible. During the final build, it would seem the debug data was left in the executable, (abet disabled), and was in a plain-text format that could be grepped with the Linux "strings" command.

|                   Filename                   |
|:--------------------------------------------:|
|          c:\ff7\chocobo\ch_app.cpp           |
|          c:\ff7\chocobo\ch_chr.cpp           |
|         c:\ff7\chocobo\ch_ddraw.cpp          |
|          c:\ff7\chocobo\ch_init.cpp          |
|         c:\ff7\coaster\psxdata_c.cpp         |
|           c:\ff7\condor\cd_app.cpp           |
|          c:\ff7\condor\cd_ddraw.cpp          |
|          c:\ff7\condor\cd_init.cpp           |
|           c:\ff7\condor\cd_tim.cpp           |
|         c:\ff7\field\src\ad_app.cpp          |
|          c:\ff7\field\src\ad_bk.cpp          |
|         c:\ff7\field\src\ad_cdr.cpp          |
|         c:\ff7\field\src\ad_data.cpp         |
|        c:\ff7\field\src\ad_ddraw.cpp         |
|        c:\ff7\field\src\ad_human.cpp         |
|        c:\ff7\field\src\ad_image.cpp         |
|         c:\ff7\field\src\ad_list.cpp         |
|         c:\ff7\field\src\ad_obj.cpp          |
|         c:\ff7\field\src\ad_pal.cpp          |
|         c:\ff7\field\src\ad_tile.cpp         |
|         c:\ff7\field\src\tutaddr.cpp         |
|          c:\ff7\highway\psxdata.cpp          |
|           c:\ff7\snobo\memory.cpp            |
|             c:\ff7\snobo\tmd.cpp             |
|        c:\ff7\src\battle\b3ddata.cpp         |
|         c:\ff7\src\battle\battle.cpp         |
|   c:\ff7\src\battle\battle3d\amptoanm.cpp    |
|     c:\ff7\src\battle\battle3d\bdata.cpp     |
|     c:\ff7\src\battle\battle3d\char.cpp      |
|     c:\ff7\src\battle\battle3d\enemy.cpp     |
|   c:\ff7\src\battle\battle3d\limitbrk.cpp    |
|      c:\ff7\src\battle\battle3d\lmd.cpp      |
|      c:\ff7\src\battle\battle3d\mdl.cpp      |
|     c:\ff7\src\battle\battle3d\stage.cpp     |
|   c:\ff7\src\battle\myoshiok\lasboss3.cpp    |
|      c:\ff7\src\battle\yama\coloss.cpp       |
|       c:\ff7\src\battle\yama\init.cpp        |
|       c:\ff7\src\battle\yama\inits.cpp       |
|     c:\ff7\src\battle\yasui\deadsef.cpp      |
|      c:\ff7\src\battle\yasui\sting.cpp       |
|     c:\ff7\src\battle\yasui\vahamut0.cpp     |
|       c:\ff7\src\credits\credfile.cpp        |
|         c:\ff7\src\main\initpath.cpp         |
|           c:\ff7\src\main\main.cpp           |
| c:\ff7\src\menu\btlmenu\english\callback.cpp |
|     c:\ff7\src\menu\english\loadmenu.cpp     |
|        c:\ff7\src\movie\sm_movie.cpp         |
|          c:\ff7\src\wm\wmdefine.cpp          |
|           c:\ff7\src\wm\wmfile.cpp           |
|       c:\lib\h\graphics\sw\offset.hpp        |
|          c:\lib\src\file\direct.cpp          |
|           c:\lib\src\file\file.cpp           |
|          c:\lib\src\file\is_lib.cpp          |
|         c:\lib\src\file\registry.cpp         |
|         c:\lib\src\file\smcdfile.cpp         |
|       c:\lib\src\graphics\directx.cpp        |
|        c:\lib\src\graphics\driver.cpp        |
|       c:\lib\src\graphics\dx_3d2d.cpp        |
|        c:\lib\src\graphics\dx_dbg.cpp        |
|       c:\lib\src\graphics\dx_graph.cpp       |
|        c:\lib\src\graphics\dx_mat.cpp        |
|       c:\lib\src\graphics\dx_mesh.cpp        |
|        c:\lib\src\graphics\dx_pal.cpp        |
|       c:\lib\src\graphics\dx_rend.cpp        |
|       c:\lib\src\graphics\dx_rend5.cpp       |
|       c:\lib\src\graphics\dx_rendi.cpp       |
|       c:\lib\src\graphics\dx_rendx.cpp       |
|        c:\lib\src\graphics\dx_sfx.cpp        |
|        c:\lib\src\graphics\dx_spr.cpp        |
|       c:\lib\src\graphics\dx_stat.cpp        |
|       c:\lib\src\graphics\dx_view.cpp        |
|        c:\lib\src\graphics\g_drv.cpp         |
|       c:\lib\src\graphics\instance.cpp       |
|        c:\lib\src\graphics\light.cpp         |
|         c:\lib\src\graphics\psx.cpp          |
|       c:\lib\src\graphics\psxgraph.cpp       |
|        c:\lib\src\graphics\render.cpp        |
|         c:\lib\src\graphics\shp.cpp          |
|        c:\lib\src\graphics\sw\sw.cpp         |
|      c:\lib\src\graphics\sw\sw_vert.cpp      |
|         c:\lib\src\graphics\sw\z.cpp         |
|          c:\lib\src\input\input.cpp          |
|           c:\lib\src\list\list.cpp           |
|           c:\lib\src\mem\heap.cpp            |
|            c:\lib\src\mem\mem.cpp            |
|          c:\lib\src\movie\movie.cpp          |
|          c:\lib\src\polygon\anm.cpp          |
|        c:\lib\src\polygon\plytopd.cpp        |
|        c:\lib\src\polygon\polygon.cpp        |
|          c:\lib\src\polygon\rsd.cpp          |
|          c:\lib\src\polygon\tim.cpp          |
|           c:\lib\src\sort\sort.cpp           |
|           c:\lib\src\sound\acm.cpp           |
|    c:\lib\src\sound\creative\sfutils.cpp     |
|         c:\lib\src\sound\dx_snd.cpp          |
|          c:\lib\src\sound\midi1.cpp          |
|          c:\lib\src\sound\sound.cpp          |
|          c:\lib\src\stack\stack.cpp          |
|         c:\lib\src\thread\thread.cpp         |
|          c:\lib\src\token\token.cpp          |
|          c:\lib\src\trans\trans.cpp          |
|                                              |

**Code list**
