---
title: "Please Remain Calm: Solving the Owl Sector ARG"
date: 2017-05-02T11:08:07-04:00
draft: false
---

My first experience with an alternate reality game was in 2004. I was a starry-eyed 14 years old freshly aboard the hype train for the new Halo game. The [theatrical trailer](https://www.youtube.com/watch?v=Zz6FNKawJBc) for Halo 2, at the time, ended with an Xbox logo directing the viewer to xbox.com, whilst also quickly flashing the text of another URL – ilovebees.com.

![An Internet Explorer screenshot of ilovebees.com](/please-remain-calm/i-love-bees.jpeg)


From that moment on I was pulled into an internet adventure unlike anything that I had ever experienced. ilovebees would set the stage for my insatiable curiosity around internet cryptography and puzzle solving.

***

Fast forward to September of 2016, five days before the release of [Rise of Iron](https://www.bungie.net/en/pub/riseofiron), Destiny’s latest expansion. [A post](http://(https//www.reddit.com/r/DestinyTheGame/comments/52xcl6/splen-%C2%A0%20dor26perk/ ) on the Destiny subreddit surfaces detailing a mysterious “infection” in the game world. Moments later, stream viewers on Twitch would discover an account named **owlsector** which subsequently linked to a bungie.net [subdomain](http://owlsector.bungie.net/).

![A Safari screenshot of owlsector.net](/please-remain-calm/owl-sector-net.png)

The following days would lead to an expansive listing of chat [logs](https://www.reddit.com/r/DestinyTheGame/comments/535jed/owlsectormegathreadpartdeuxigotafeverand/ ) posted to Owl Sector, detailing a mysterious backstory behind the infection that had shaken the fictional world of Destiny.

Rise of Iron released the following week and most Owl Sector talk casually disappeared. Days later, the community would throw themselves at the new raid, Wrath of the Machine. As teams began to be cross the finish line, players began to discover hidden [monitors](https://i.ytimg.com/vi/MsJ8fBid0iQ/maxresdefault.jpg) scattered throughout the raid itself. It was quickly discovered that these monitors were inexplicably linked to a chest room in the final boss chamber. This chest room was guarded by five laser grids.

Simultaneously, a link to yet another bungie.net [page](https://www.bungie.net/en/net/sim) was posted to the Owl Sector site. This link directed to a page simply titled “Sim.” When navigating to Sim, the webpage would return sets of data in the form of nodes, glyph sequences, and alphanumeric strings. Also included was a data dump specifying that additional nodes in the sequence were required.

These were just the first few happenings of what would end up being a massive ARG implemented to launch with Rise of Iron by Bungie. This puzzle led to a final prize — the exotic pulse rifle, Outbreak Prime. With the help of many a Redditor, Math Class would ultimately be the first clan to obtain the weapon.

This is how we did it.

***

After a late night of data collection with my clanmates, I’d wake up to go to work. While at the office and still consumed by the puzzle, I took to Reddit to see what the community had dug up. Thread after thread detailed what each internet persona believed they had found. There were users posting screenshots of their unique SIM page, Pastebin links to their copied node information, and even recreations of what they were seeing recreated in Microsoft Word. It was a mess.

The lack of consistently formatted data was obvious. And frustrating.

I created a Reddit thread linking to a Google Form that I had been using to track data from the prior night. I also created a redirect from a domain I owned, owlsector.net (long story), to that same form. In the thread, I explained that data was going to be key and without coming together we would never break through to whatever the next steps could be. The thread took off and entries began to pour in by the hundreds.

Admittedly, I had no idea what I was getting into. Thanks to Reddit, my form would ultimately collect over 15,000 unique data entries. Without this community provided data, the puzzle would have been impossible to solve. It was also through this Reddit trawling that I saw a post from /u/mg2brandon. I thought he was onto something. We made quick introductions over private message and then immediately progressed the third base — an invite to the Math Class Slack.

***

There were several important data related variables that had to be accounted for, collected, organized, and standardized. The data points we collected were:

* Original Node1 
* Original Node2 
* Original Node3 
* Original Node4 
* Original Node5 
* Summary of Original Node 
* Mutated Node1 
* Mutated Node2 
* Mutated Node3 
* Mutated Node4 
* Mutated Node5 
* Summary of Mutated Node 
* Provided Processing Key 
* Provided Initialization Vector 
* Provided Unprocessed Information

![A Safari screenshot of spreadsheet node data](/please-remain-calm/node-data.jpeg)

Our first big break came from following the inferred numeric forwarding protocol.

By following each transformation hop-by-hop we could assemble keys from the data of eight individual users.The ARG page had hinted at the use of [Rijndael encryption in CBC mode](https://en.wikipedia.org/wiki/AdvancedEncryptionStandard) (it literally said “Node sensors have detected unprocessed information [Rijndael-AES-CBC]”) and there were now eight key fragments that were each 32 bits long. So, Brandon attempted AES-256 decryption and was rewarded with a cryptic JPEG image:

![A large square surrounded by several other small shapes](/please-remain-calm/puzzle-piece.png)

Applying the same technique to the other known sequences quickly resulted in a dozen more images. But, it wasn’t clear yet how they were interrelated and the vast majority of our data was still unable to be decrypted.

For context, these breakthroughs all happened within a span of around four hours. The next four hours would lead to Brandon and I agonizing over what we were doing wrong. The lion’s share of data we were trying to decrypt was leading nowhere.

The big break came when Reddit user /u/MockingDolphin posted an [analysis](https://www.reddit.com/r/DestinyTheGame/comments/54rv64/argnodetransformationswehavebeendoingthem/ ) of how we’d been misapplying the non-numeric forwarding protocols. In other words, we’d been trying to transform the wrong node.

Brandon got to work on an updated decryption pipeline and quickly produced around 900 new tiles. Our heads exploded. This was an insane amount of visual data. But it still wasn’t obvious how, or if, we were supposed to fit these tiles together in any meaningful way. Another break came when /u/ZephyrFoxworth [commented](https://www.reddit.com/r/DestinyTheGame/comments/54rv64/argnodetransformationswehavebeendoingthem/d84pn2x/ ) with an observation about the symbols on the edges of diagonally-adjacent tiles.

![Matching the strange, puzzle like, node shapes to one another](/please-remain-calm/matching-pieces.png)

For example, if Tile A had ●◆ on its right side and Tile C had ●◆ on its left side, we could order them on the grid as ABC without any regard for Tile B. The result, it turns out, is a scrambled checkerboard. We needed to establish a set of directly neighboring tiles to stitch the checkerboard into a complete map, so Brandon manually placed four tiles onto a grid as neighbors:

![A large square surrounded by several other small shapes](/please-remain-calm/abc-matches.png)

Using those tiles as a starting point, we could now assemble an imperfect, but discernible, image.

![A large square surrounded by several other small shapes](/please-remain-calm/node-assembly.gif)

It was a map of the diamond room in Wrath.

***

From here, the story shifted to involve Datto and crew. It is a Tuesday, the normal raid night stream was up and Math Class were throwing themselves at Wrath.

I messaged Datto in our TeamSpeak:

> you need to end the stream now, like right fucking now.

> wtf

> we have it

I linked him the mostly assembled image of the diamond room. He instantly understood.

While Datto wound the stream down, the clan began assembling another crew together into the raid and test our map. I joined in on that group while Datto pulled in Brandon. After a few wipes (the raid was still new!), we made it to the diamond room around the same time as the other group and began putting our map theories to the test.

The rest is history.

***

![A large square surrounded by several other small shapes](/please-remain-calm/brandon-activating.png)

Datto and Brandon’s crew would be the first raid group in the world to open the diamond. Inside was the fifth monitor and a chest. After Aksis was defeated, that same group would check the hidden room underneath the boss chamber. The full laser grid was deactivated and the chest was able to be picked up. Once opened, the Outbreak Prime quest officially kicked off in the game world.

The next few hours would be a series of steps outlined by the in-game quest — most including some sort of math puzzle. At the end of it all was Outbreak Prime. Outhouse would be the first Guardian in the world to add it to his inventory.

> Suck it, nerds!

The Owl Sector ARG was a master class in puzzle solving. It required Guardians of all walks and locales to assemble, communicate, and journey through a cryptographic frenzy. Together.

After the dust settled, Brandon would become part of Math Class. We’ve been great friends ever since.

Whatever you may think of Bungie games, it’s undeniable that the worlds they build have the inherent ability to bring humans together in inspiring and interesting ways. For that, they have my eternal gratitude.
