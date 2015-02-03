#     _             _     _ _  ___ _       _
#    / \   _ __ ___| |__ (_) |/ (_) |_ ___| |__   ___ _ __
#   / _ \ | '__/ __| '_ \| | ' /| | __/ __| '_ \ / _ \ '_ \
#  / ___ \| | | (__| | | | | . \| | || (__| | | |  __/ | | |
# /_/   \_\_|  \___|_| |_|_|_|\_\_|\__\___|_| |_|\___|_| |_|
#
# Copyright 2014 Łukasz "JustArchi" Domeradzki
# Contact: JustArchi@JustArchi.net
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

You can add your own cleaning lists here.

Every cleaning list may contain two files inside:
- clean.txt -> Files/folders from this list will be moved to $ACTIVE_PROJECT/bloatware folder. They WILL be included in output .zip but WON'T be flashed. "Bloating" after debloating is possible.
- remove.txt -> Files/folders from this list will be removed permanently from the $ACTIVE_PROJECT. "Bloating" is not possible after debloating.

So if you want to give your users freedom in restoring APKs from output .zip, i.e. through AROMA. Use clean.txt
If you simply want to remove permanently bloatware from your ROM, use remove.txt

You may also use both clean.txt and remove.txt. For example I'm using such combination for removing all installable Google APKs from the market while only cleaning Samsung APKs.

ArchiKitchen currently supports:
1. Empty lines []
2. Commented lines [# This is comment] [#This as well]
3. Apks [Myapp.apk] [Chrome.apk]
4. Libs [mylib.so] [libchromeview.so]
5. Jars [kies.jar] [framework2.jar]
6. Absolute paths [/system/media/audio/awesome.ogg] [/system/csc]
7. Wildcards [Google*.apk] [/system/media/*.ogg]

RULE OF THUMB: One entry per line

Please note that:
- Apks and Jars also include cleaning of proper .odex files connected with them. If you specify absolute path, odex files won't be cleaned, unless you use a wildcard like /system/app/Chrome*
- It's better to use i.e. Chrome.apk instead of /system/app/Chrome.apk, because Chrome.apk entry apart from cleaning odex will also clean both /app and /priv-app locations
- In general, try to not use absolute paths if you can achieve the same using built-in rules. Unless you REALLY want to delete only one specific file/folder and not anything else
- Wildcards apply to all rules above, so you can specify i.e. libDio*.so instead of /system/lib/libDio*.so (both will work)
- Take care with wildcards and absolute paths. Try to use bare-minimum wildcards like /system/etc/hidden_apks_list_*.txt instead of /system/etc/hidden*

For example, a remove.txt with following content:
---------------------------------
# My awesome cleaning list v 1.1
# Here we start

/system/csc
/system/audio/file.ogg
Chrome.apk
libchromeview.so
kies.jar
---------------------------------
Will result in removing:
/system/csc (directory)
/system/audio/file.ogg
/system/app/Chrome (directory)
/system/app/Chrome.apk
/system/app/Chrome.odex
/system/priv-app/Chrome (directory)
/system/priv-app/Chrome.apk
/system/priv-app/Chrome.odex
/system/lib/libchromeview.so
/system/framework/kies.jar
/system/framework/kies.odex
