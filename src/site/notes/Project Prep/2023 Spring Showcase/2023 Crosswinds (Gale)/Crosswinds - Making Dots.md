---
{"dg-publish":true,"permalink":"/project-prep/2023-spring-showcase/2023-crosswinds-gale/crosswinds-making-dots/"}
---


## Create the Dots Sprite

Make a dots sprite. This will be for the first player, who is trying to make lines that go left to right. 
ドット スプライトを作成します。これは、左から右へのラインを作成しようとしている最初のプレーヤー向けです。

A good costume for this is a triangle going right like this "🚩". It should be pretty small, say about 10 x 10 pixels. 
この「🚩」のように直角三角形が良い衣装です。かなり小さく、たとえば約 10 x 10 ピクセルにする必要があります。

When we receive the `when I receive [make dots v]` broadcast, we will "make" the dots. There will be 4 rows and 5 columns of dots.
{ .hasInlineScratch }
 `when I receive [make dots v]` ブロードキャストを受信すると、ドットを「作成」します。 4 行 5 列のドットがあります。
{ .hasInlineScratch }



## Creating the Dot Clones

### Row 1
Let's make the first row. We go to the position of the first dot. In this case it will be `x: (-100) y: (125)`.
最初の行を作成しましょう。最初のドットの位置に行きます。この場合は「x: (-100) y: (125)」となります。

Then we make a copy of the sprite, a **clone**. Think of these as *baby* sprites, and our normal sprite is the *mother* sprite. It will show up right there (though it will cover our mother sprite.)
次に、スプ​​ライトのコピー、**クローン**を作成します。これらを *baby* スプライトと考えてください。通常のスプライトは *mother* スプライトです。すぐそこに表示されます (ただし、マザー スプライトをカバーします)。

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
go to x: (-100) y: (125)
create clone of [myself v]
~~~
``` 

Now we do the same thing, but first we move 50 pixels to the right. That means `x` changes from -100 to -50. `y` stays the same.
次に同じことを行いますが、最初に 50 ピクセル右に移動します。これは x が -100 から -50 に変化することを意味します。 y はそのままです。

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
go to x: (-100) y: (125)
create clone of [myself v]
go to x: (-50) y: (125)
create clone of [myself v]
~~~
``` 


Do this 3 more times, changing `x` by 50 each time. 
x を 50 ずつ変えながら、これをあと 3 回繰り返します。



Now the first row has 5 clones, all at `y` = 125.
最初の行には 5 つのクローンがあり、すべて `y` = 125 です。

### A Better Way: A Loop for Columns


But there is a better way to do this. 
しかし、これを行うためのより良い方法があります。

It would be nice if we could do something like this:
次のようなことができればいいのですが:

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
repeat (5)
go to x: (-100) y: (125)
create clone of [myself v]
end
~~~
``` 

The problem is that this would put all 5 clones in the same place. Repeating is good, but we want to **repeat with a small change**. `x` has to change each time through the loop. 
問題は、これにより 5 つのクローンすべてが同じ場所に配置されることです。繰り返すのは良いことですが、**小さな変更を加えて繰り返す**必要があります。 x はループのたびに変更する必要があります。

Luckily, there's a trick that will help us. 
幸いなことに、私たちを助けるトリックがあります。

If you have a number in your code, you can replace that number with a variable. In this case, the number is -100. That's the number that changes in the repeat loop. 
コードに数字がある場合は、その数字を変数に置き換えることができます。この場合、数値は -100 です。それが繰り返しループで変化する数です。

Create a variable called `(x value)`. Make sure it is a **for this sprite only** variable. This will make sure only this sprite uses these variables.
{ .hasInlineScratch }
「(x 値)」という変数を作成します。 **このスプライト専用**の変数であることを確認してください。これにより、このスプライトのみがこれらの変数を使用するようになります。
{ .hasInlineScratch }

The first thing we do is set the variable to the starting number.
最初に行うことは、変数を開始番号に設定することです。

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
set (x value) to (-100) 
repeat (5)
go to x: (-100) y: (125)
create clone of [myself v]
end
~~~
``` 

Then we use the variable instead of the number where it appears. 
次に、変数が表示される数値の代わりに変数を使用します。

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
set (x value) to (-100) 
repeat (5)
go to x: (x value) y: (125)
create clone of [myself v]
end
~~~
``` 


So far this doesn't help us. But, at the end of the loop, we can change `(x value)` after creating the clone. Now each time through the repeat loop, the `(x value)` changes.
{ .hasInlineScratch }
これまでのところ、これは役に立ちません。しかし、ループの最後で、クローンを作成した後で `(x value)` を変更できます。これで繰り返しループのたびに `(x value)` が変化します。
{ .hasInlineScratch }

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (x value) to (-100) 
repeat (5)
go to x: (x value) y: (125)
create clone of [myself v]
change [x value v] by (50)
end
~~~
``` 

The first time it is -100, then -50, then 0, then 50, then 100. This is what we want.
最初は -100、次に -50、次に 0、次に 50、そして 100 です。これが私たちが望むものです。

Why do we do this? 
なぜこれを行うのか
1. The code is shorter. If there is a lot of code in the loop, this can make it much shorter. コードが短い。ループ内に多くのコードがある場合、これによりループが大幅に短縮されます。
2. The code is easier to adjust. For example, if we decide we want 6 columns, we just have to change the number 5 to 6 (and maybe adjust the starting `(x value)` or the amount of change). コードの調整が容易になります。たとえば、6 列が必要だと判断した場合、数字の 5 を 6 に変更するだけで済みます (さらに、最初の `(x 値)` または変更量を調整することもできます)。 { .hasInlineScratch }

### Row 2
Can you make the next row? Again, we want to create 5 more clones the same way, but make y = 75. Use a repeat loop if you can.
次の行を作ることができますか

### Rows 3 and 4
After that we need 2 more rows, one with y = 25 and one with y = -25. 
その後、さらに 2 つの行が必要です。1 つは y = 25 で、もう 1 つは y = -25 です。

You should now have 4 rows of 5 dots each. 
これで、それぞれ 5 つのドットの 4 つの行ができたはずです。

### A Better Way: A Loop for Rows

Did you notice that when we created the four rows we had another example of **repeating something with a small change**. This time `(y value)` changes. If you want to make your code better, you could use the same trick above. The first step is to make a variable called  `(y value)`, and set it to its starting value, -125. Again, make sure it is a **for this sprite only** variable.
{ .hasInlineScratch }
4 つの行を作成したときに、**小さな変更を加えて何かを繰り返す**別の例があったことに気づきましたか。今度は `(y value)` が変わります。コードを改善したい場合は、上記と同じトリックを使用できます。最初のステップは、「(y 値)」という変数を作成し、それを開始値 -125 に設定することです。繰り返しますが、**このスプライト専用**の変数であることを確認してください。
{ .hasInlineScratch }

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to (-125) 
...

~~~
``` 

Then we will add a repeat loop around **ONE of the row loops** code. The red part is JUST the code for the **FIRST ROW** you created above. 
次に、**1 つの行ループ** コードの周りに繰り返しループを追加します。赤い部分は、上で作成した **FIRST ROW** のコードです。


```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to (125) 
repeat (4)
the code for FIRST ROW goes here ::custom #F00
end
~~~
``` 

Then, we use the variable in the places where  `(y value)` appears.
{ .hasInlineScratch }
そして、「(y 値)」が現れる場所で変数を使用します。
{ .hasInlineScratch }


```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set [y value v] to (125) 
repeat (4)
the code for the FIRST ROW with (y value) ::custom #F00
end
~~~
``` 

And last, at the bottom of the repeat loop, change `(y value)`.
{ .hasInlineScratch }
そして最後に、繰り返しループの一番下で、「(y 値)」を変更します。
{ .hasInlineScratch }

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to (-125) 
repeat (4)
the code for the FIRST ROW with (y value) ::custom #F00
change [y value v] by (-50)
end
~~~
``` 

## Hiding and Showing the Dots

### Hide on creation
We are creating the dots in the **Setting Up** stage pf the project. We will create the clones only once for the whole game. 
プロジェクトの **セットアップ** 段階でドットを作成しています。ゲーム全体で一度だけクローンを作成します。

We want each clone to be hidden when it is created. We will only show them during the game loop, after the player has been chosen. So, we hide them when they are created:
各クローンは、作成時に非表示にする必要があります。プレイヤーが選択された後、ゲームループ中にのみ表示されます。したがって、作成時に非表示にします。

```ad-scratch
title: 
~~~scratchblock
when I start as a clone
hide
~~~
``` 

### Show after player chosen

If you look at the code for each player, once the player is chosen, we broadcast **show current player**. 
各プレーヤーのコードを見ると、プレーヤーが選択されると、**show current player** をブロードキャストします。

```ad-scratch
title: Player 1 sprite
~~~scratchblock
when this sprite clicked
hide
set [CURRENT PLAYER v] to [1]
broadcast [show current player v] and wait

~~~
``` 

That's the moment we want the clones to appear in the game loop.
これが、クローンをゲーム ループに表示させたい瞬間です。
```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [show current player v]
show
~~~
``` 


### Hiding in Start Game Loop

However, once the round is finished, we go back to the **start game loop** position. We have to hide the dots at this point, so that they are hidden when we choose the player. So we add this:
ただし、ラウンドが終了すると、**ゲーム ループの開始**の位置に戻ります。この時点でドットを非表示にして、プレーヤーを選択したときにドットが非表示になるようにする必要があります。したがって、これを追加します。

```ad-scratch
title: Dots 1
~~~scratchblock

when I receive [START GAME LOOP v]
hide

~~~
``` 

### Hiding the Mother

One last thing. We don't want to see the mother sprite. She is just there to watch and make babies. So we hide her right away, in the receive make dots routine. 
最後に一つだけ。マザースプライトは見たくありません。彼女は赤ちゃんを見て、作るためにそこにいます。そのため、make dot ルーチンの受信で、すぐに彼女を非表示にします。

Careful:
気をつけろ：
* This is not a new stack, but make dots stack we created above.これは新しいスタックではありませんが、上記で作成したドットスタックを作成します。
* Remember, the grey dots mean "the code that is already there". We are putting the hide block right after the receive block and before the other code. 灰色の点は「既に存在するコード」を意味することに注意してください。 hide ブロックを receive ブロックの直後、他のコードの前に置きます。

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
hide
...
~~~
``` 
## Dots 2

Player 1 now has his dots. Player 1 is going right to left. But we need a second set of dots for player 2. He is going top to bottom. 
プレイヤー 1 はドットを持っています。プレーヤー 1 は右から左に移動します。しかし、プレイヤー 2 には 2 番目の点のセットが必要です。彼は上から下に向かっています。

Player 2's dots are almost the same. To start, just **duplicate the entire sprite**.
プレイヤー 2 のドットはほぼ同じです。まず、**スプライト全体を複製**します。

But we have to make some changes. Here are the differences:
しかし、いくつかの変更を加える必要があります。違いは次のとおりです。

* This time the costume is a down arrow  🔻
 * 今回の衣装は下向き矢印です🔻
* Make it a different color.
- 別の色にします。
* 4 columns of dots per row, and 5 rows! 
* 1 行あたり 4 列のドット、および 5 行!
* The start x and y values are different:
* 開始の x と y の値が異なります。
	* `(x value)` = -75 { .hasInlineScratch }
	* `(y value)` = 150 { .hasInlineScratch }

If you used repeat loops, it will be quick and easy. If not, not so quick and easy.
繰り返しループを使用すると、すばやく簡単に実行できます。そうでない場合は、それほど迅速かつ簡単ではありません。


## Good Job!

That's it. Good job!
それでおしまい。よくできた！