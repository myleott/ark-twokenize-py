ark-twokenize-py
================

This is a crude Python port of the [Twokenize class from ark-tweet-nlp](https://github.com/brendano/ark-tweet-nlp/blob/master/src/cmu/arktweetnlp/Twokenize.java).

It produces nearly identical output to the original Java tokenizer, except in a
few infrequent situations. In particular, Python does not support partial
case-insensitivity in regular expressions and this causes some tokenization
differences for ``Eastern" style emoticons, particularly when the left and right
halves are of different cases. For example:

    Java (original): v.V
    Python (port): v . V

Emoticons of this kind are seemingly pretty rare. Nevertheless, I have included
a fix for one special case:

    Java (original): o.O
    Python (port, w/o fix): o . O
    Python (port, w/ fix): o.O

Evaluation
----------

A comparison on 1 million tweets found 83 instances (0.0083%) where tokenization
differed between the original Java version and this Python port. The differences
were primarily related to the emoticon issue discussed above, and it was not
clear in general which output was more desirable. For example:

    Text:
    Profit-Taking Hits Nikkei http://t.co/hVWpiDQ1 http://t.co/xJSPwE2z RT @WSJmarkets

    Java (original):
    Profi t-T aking Hits Nikkei http://t.co/hVWpiDQ1 http://t.co/xJSPwE2z RT @WSJmarkets

    Python (port):
    Profit-Taking Hits Nikkei http://t.co/hVWpiDQ1 http://t.co/xJSPwE2z RT @WSJmarkets
