---
layout: post
title: "Creating a Homebrew tap"
date: 2020-07-05
excerpt: "How to create a Homebrew tap"
tags: [homebrew, homebrew-tap, brew]
comments: false
---

## CREATING A HOMEBREW TAP

Sometimes, you might come across a need to create your own tap for [Homebrew](https://github.com/Homebrew/brew), either to host your own tools or for formulae that you tweaked as per your needs.
I stumbled upon this path when I was trying to install a deleted formula, and there would be others in my team who would need to do the same.
To my surprise, creating a Homebrew tap was surprisingly easy.

### Create a Git repository

Create a Git repository that is named starting with `homebrew-`. This ensures that the short `brew tap` command can be used.
An easy way to create a new tap is by using the `brew tap-new` command:
```
brew tap-new aditig/tools
```
This creates a new tap along with some template files:
```
aditig
└── homebrew-tools
    ├── Formula
    └── README.md
```

### Add a formula

You can now add a formula `myformula.rb` to the `Formula` subdirectory.
We'll not be going into the details of how to write a formula, but a simple formula could look like this:
```
class MyFormula < Formula
  desc "My formula"
  homepage "https://myformula.com"
  url "https://myformula.com/myformula_1.0.tar.gz"
  sha256 "<sha256>"

  def install
    system "make", "install"
  end

  test do
    system "#{bin}/myformula", "--help"
  end
end
```

### Use the tap

To tap the repository:
```
brew tap aditig/tools <git-clone-url>
```
If you're using Github, you can skip the URL.

You can now install the formula:
```
brew install myformula
```
If there are naming conflicts with another formula of the same name, provide the tap details:
```
brew install aditig/tools/myformula
```


As you can see, it's straight-forward to create a Homebrew tap. 
For an example, look at [homebrew-tools](https://github.com/aditig/homebrew-tools).
The [Homebrew documentation](https://docs.brew.sh) includes more details on how to maintain a tap and writing new formulae.