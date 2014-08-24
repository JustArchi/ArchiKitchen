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
3. Absolute paths [/system/media/audio/awesome.ogg] [/system/app/Myapp.apk]
4. APKs [Myapp.apk] [Chrome.apk]
5. Libs [mylib.so] [libchromeview.so]
6. Wildcards [Google*.apk] [/system/media/*.ogg]

RULE OF THUMB: One entry per line

For example, a remove.txt with following content:
---------------------------------
# My awesome cleaning list v 1.0
# Here we start

/system/audio/file.ogg
Chrome.apk
libchromeview.so
---------------------------------
Will result in removing:
/system/audio/file.ogg
/system/app/Chrome.apk
/system/app/Chrome.odex
/system/priv-app/Chrome.apk
/system/priv-app/Chrome.odex
/system/lib/libchromeview.so