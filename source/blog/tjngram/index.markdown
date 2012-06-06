---
layout: page
title: "TJNgram"
date: 2012-06-06 17:32
comments: true
sharing: true
footer: true
---

TJNGram is a N-Gram generator in Ruby, supporting English, Chinese, Janpanese and Korean.

It's common to see Chinese, Jananse and Korean articles contain some English, but it's not common to see an n-gram library which can parse this sort of articles. TJNGram was made for solving this problem.

*   [Github](https://github.com/tonytonyjan/TJNGram)
*   [RugyGems](https://rubygems.org/gems/TJNGram)

## Install

    gem install tjngram

## Usage

    require 'tjngram'

    text = <<eos
    這是一個範例。
    This is an example.
    これは例です。

    這裡有一個蘋果。
    There is an apple.
    これはリンゴです。
    eos

    puts text, "=========="

    TJNGram.process(2, text) #=> {"一個"=>2, "これ"=>2, "is an"=>2, ...}
    
## Note

If your file is utf-8 encoded, please run ruby with the following options:

    ruby -Ku example.rb

It's strongly recommand you make your all script files utf-8 encoded.
