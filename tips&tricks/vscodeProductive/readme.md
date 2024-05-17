# Become More Productive Course

This course is on freeCodeCamp [channel](https://www.youtube.com/watch?v=heXQnM99oAI), titled: `VS Code Tutorial – Become More Productive`

> Quick overview of what's Vscode

![basic naming](image.png)

* After we open any activity bar item, we'll see the `sidebar` or it!

![alt text](image-4.png)

* the title of opened file above our editor is called `tab`

![tab](image-1.png)

* the hierarchy code is called breadcrumbs

![breadcrumbs](image-2.png)

* the little code mapping on the right is called the `mini-map`

![mini-map](image-3.png)

* and the container of terminal and its siblings is called panels

![panels](image-5.png)

## hidden stars in Vscode

many of the hidden star stuff in Vscode are in the panels

> 1st essential tool to using Vscode (Command Palette)

With using Command Palette `ctrl + shift + P`, we can hide both status bar and activity bar: by doing:

```sh
>status bar visibility # view: status bar visibility
>activity bar # view: Hide Activity bar
# 🔴These both are great in tutoring🔴
>breadcrumbs # view: toggle breadcrumbs
>tab # toggle tab visibility
```

There are many awesome commands to use rapidly, as `new` which opens options to add new files to current directory, and `git` which appears all sub-commands to git, **and a great one** is: `snippet`, it appears fast fillings `snippets: insert snippet` as when using emmets: check snippet in js files, or even here in md files for example!

## installing themes 15:37

Extensions are critical to unleash productivity in Vscode, check its marketplace [here](https://marketplace.visualstudio.com/vscode), and search for `theme`

although, you can read about themes in Vscode's docs [here](https://code.visualstudio.com/docs/getstarted/themes)

There is a blue background theme similar to what I use called: `Winter is coming theme`. `night owl` is better

but a better way is to use `ctrl + shift + x` for extensions!

open palette then type: `theme`, it'll output themes to use in installed extensions

Download the `material icon theme` to have nice icons in the explorer sidebar

some most popular themes are:

* dark purple:
  * One dark pro
  * Dracula
  * atom one dark

* black average
  * github
  * winter is coming
  * night owl
  * Monokai pro => many good choices `paid`

* purple purple
  * shades of purple

* Yellow blue
  * cobalt2

* popular similar to atom's default and other editors
  * material theme

those are the most popular in 23

---

> less popular themes

1. PaleNight theme
1. SynthWave '84
1. nord (too plain)
1. panda
1. Tokyo night
1. rainglow (liked it)
1. moonlight 2 (good)
1. horizon
1. bearded theme (vivid is good)
1. cyberPunk

## font settings 32:00

Other than adding extensions, changing settings is the second major approach to modify needed experience.

There are two recommended fonts by Chris Sev, which you can download here:

* [Cascadia-code](https://github.com/microsoft/cascadia-code)
* [Fira Code](https://github.com/tonsky/FiraCode)

they're monospaced fonts, traditionally the best for coding he said!

second one has ligatures, which is connecting => to appear as arrows ➡️, and other things as not equals etc...

### change editor's font

access settings `ctrl + ,`, there are two approaches to open settings, `json` and `UI`, simply via palette, `>open settings`

we'll choose ui approach for now, then search for `font family`
then in the edit input, add `'Cascadia Code', ` in the beginning, as css

> Microsoft added 1st font to installed by default in vscode fonts

Installing fonts is as installing system fonts, simply open the files themselves to add them to fonts directory

A paid font `Chris Sev` uses is:

* Operator Mono Lig $175 - $200

![money isn't an issue!](image-6.gif)

He's used `Comic Sans MS`

[This](https://coding-fonts.netlify.app/fonts/codelia/) is a good place to check fonts for coding, they're plenty of good fonts over there!

> I loved `Comic Code` in that site! it's pricy

### other font settings

* font size
* line height
* font ligatures

for line height, to get 1.6 we multiple `tended-height*font-size`, as `1.6*14`

type ligatures in the search bar, it'll ask you to change its value in json file!

![that's awesome](icegif-908.gif)

there's another good feature for modifying font-size through zooming with the mouse, which is `mouse wheel zoom`, you can activate it from the settings

## Chris Sev's 5 favorite fonts

same page we used for [fonts](https://coding-fonts.netlify.app/fonts/codelia/) include those monospace (same amount of width) fonts:

1. operator mono (paid) $200
1. Cascadia Code (started using it)
1. fira code
1. Inconsolata
1. Anonymous Pro (free)
1. comic code

## Vscode appearance settings

1. Tab size, comes with insert spaces {default: true}
2. rulers {commonly: 80} appears a line to notify us!
3. Render Indent Guides {default: true}, `lines between tabs`
4. word wrap: `alt + z`
5. cursor blinking

the little border-left aside to some settings means that you changed them from their defaults

## Vscode Home base 55:55

### Getting files into Vscode

* dragging the folder directly into the explorer sidebar panel
* Nav options => file => open file || open in the starting window || ctrl + O
* palette => file open

### Creating files && folders |> Explorer

* ![icons](image-8.png) to create a folder, click the left one then `newDir/newName` at once! 💌 I said it
* dragging root/file => subDir
* ![circle](image-7.png)  is when you move files outer the Vscode && return current open file to focus👍
* ![this](image-6.png) to collapse everything

### Context Menu

* 🖱️ right click => `Reveal in File Explorer/FinderForMac` || `ctrl + shift + R`
* ❤️ Open in Integrated Terminal |> I like this and needed it!❤️
* rest are normal, check them out!

### hidden tools

Outline, turns out to be useful! it appears nested objects as breadcrumbs functionality.![breadcrumbs sister](image-10.png)

We can sync it with our cursor with ... aside it then activating the option `Follow Cursor`

### advanced new file extension

install the second option with its slogan: create files anywhere in your etc...

![advanced new file](image-11.png)

Then Open the palette `>advanced new file` it's a great tool!

Because it uses fuzzy search similar to autocompletion

> this section included most 2nd important section in vscode

## Where the magic happens

### Vscode's Editor Area

we toggle the side bar with `Ctrl + B`, while explorer opens with `Ctrl + shift + E`

We can click on the breadcrumbs to access their nested code

min-map is draggable as known to me!

We can do side by side as known to me, with two approaches, one to drag the file to the left of the screen, second is to type: `Ctrl + Alt + arrows < / > `
another way is to click on this icon:
![Split Editor](image-12.png)

we can split the same file to reference another part while editing! good idea

in newer versions we're able to split the screen on top bottom left right, as this:

![splitting](image-13.png)

to convert the split icon to top/bottom `hold alt/option for mac`

![check it out](vscodeSplitter.png)

splitted screens are called `editor groups`

check this:

![wow](image-14.png)
