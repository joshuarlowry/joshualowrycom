---
title: Algorithms to Live By- Bucket Sorting Laundry
date: "2017-04-05"
categories: 
  - design
  - motivation
description: I am currently listening (Audibling?) to the book \"[Algorithms to Live By-The Computer Science of Human Decisions](https://www.amazon.com/Algorithms-Live-Computer-Science-Decisions-ebook/dp/B015CKNWJI/ref=tmm_kin_swatch_0?_encoding=UTF8&qid=&sr=)\" written by Brian Christian and Tom Griffiths. In the book, they describe how algorithms used in computer science can also be used in the real world.
coverImage: algorithmstoliveby.jpg
---

I am currently listening (Audibling?) to the book "[Algorithms to Live By: The Computer Science of Human Decisions](https://www.amazon.com/Algorithms-Live-Computer-Science-Decisions-ebook/dp/B015CKNWJI/ref=tmm_kin_swatch_0?_encoding=UTF8&qid=&sr=)" written by Brian Christian and Tom Griffiths. In the book, they describe how algorithms used in computer science can also be used in the real world.

The next time I followed my usual laundry process, I realized that I had used something similar to the [Bucket Sort](https://en.wikipedia.org/wiki/Bucket_sort).

## Laundry Bucket Sort

### Step 1: Define the buckets.

For numbers, your buckets might be everything between 1 & 10, 11 & 20, 21 & 30, etc. For books, your buckets might be delineated alphabetically by author, e.g. Bucket 1 = Jane Austen, Louisa May Alcott; Bucket 2 = Dave Barry; etc.).

For laundry, I have come up with the following bins:

1. Hangers
2. Shirts/Dresses that hang
3. Pants that hang
4. Shirts that are folded
5. Shorts
6. Under-garments
7. Miscellaneous

\[gallery ids="377,378,379,380" type="square" columns="4"\]

### Step 2: Scatter... AKA Bin everything

Self-explanatory, and perhaps the least fun part of the system. Let me know if anyone has an algorithm for improving this ;-)

### Steps 3 & 4: Sort & Gather

After everything is binned, I systematically go through each bin and perform the necessary operation. Each bin follows the same operation, which allows for a natural flow to be achieved.

As a result of using this algorithm, I've made several improvements to our laundry management system.

1. Under-shirts are a folded shirt, however, they don't need to be in a particular order. Simply grab the shirt on both sides under the arm-pit and lift ( the result is a half fold). Stack the shirts then place them straight into the dresser as-is. It is very easy to get a dress shirt, just pick up the one on the top.
2. I only have one type of work sock, and one type of fitness sock. Why pair them when you can just stack them and take the top two to get dressed? This simplifies the folding process and the storage process.

I suppose the next step is to divide these bins into two each, one for me and one for my wife. That way, each stack goes neatly into the closet without having to think about which side of the closet I should face when putting clothes away.

What algorithms do you live by?

_Thoughtfully edited by Patricia Lowry_
