---
layout: post
uuid: 0474a7be-72a9-40f2-8dfe-d25455dfbb94
title: licensing
---

I started hacking on code that I want to publish soon, so I read enough to get a
simple introduction to the various [free software licences][licences]. The GPL
[v2][gpl] and [v3][gpl3] and [apache][apache] licenses all seemed needlessly
complicated. The MIT and BSD licences were nice and short, and very similar.
Someone else noticed the similarities and merged those two to the [ISC][]
license, which is what I am settling for now. It is very permissible (read: not
[copyleft][]).

The choice was influenced by [The Failure of the GPL][failure], which examines a
particular case which looked like a win for the GPL but in the author's opinion
was not. My inner pragmatist and idealist were arguing over [copyleft][], but
changes in how I act ( favoring simplicity and faith in the natural order of
things) meant the idealist won. One downside to the [ISC][] is that it does not
enforce anyone using my code to show me any improvements they make on it. The
other downside is that it falls under the OSI category of '[Licenses that are
redundant with more popular licenses][osi]', but it's so simple that if anyone
wanted to use my code could do so easily.

[licences]: http://en.wikipedia.org/wiki/Free_software_license
[failure]: http://www.informit.com/articles/article.aspx?p=1390172
[copyleft]: http://en.wikipedia.org/wiki/Copyleft
[gpl]: http://www.gnu.org/licenses/old-licenses/gpl-2.0.html
[apache]: http://www.apache.org/licenses/LICENSE-2.0
[gpl3]: http://www.gnu.org/licenses/gpl.html
[isc]: http://en.wikipedia.org/wiki/ISC_license
[osi]: http://www.opensource.org/proliferation-report
