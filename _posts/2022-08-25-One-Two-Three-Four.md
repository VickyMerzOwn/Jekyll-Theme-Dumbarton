---
layout: post
title:  "One, Two, Three, Four"
description: "A reflection of content covered in the first four lectures of CS553 - Cryptography, Monsoon '22"
date:  2022-08-25 08:30:00 +0530
type: card-img-top
categories: latin text
image: 
caption:
last-updated: 2022-08-25 08:30:00 +0530
categories: CS553-Monsoon'22
tag: IIT-Bhilai
author: Satvik Vemuganti
card: 
---

#### Why?

    My bad habits lead to late nights endin' alone
    Conversations with a stranger I barely know
    Swearin' this will be the last, but it probably won't
    I got nothin' left to lose, or use, or do

Been meaning to write this up for a while now. But then I'm a master procraaaaastinator, as lazy as one can imagine. Anyways, the title reminds me of this song [<u>Bad Habits - Ed Sheeran</u>](https://www.youtube.com/watch?v=orJSJGHjBLI) (cuz it starts with a soft one, two, three, four). Trust me that isn't what this blog is about. I'm simply obsessed with this song RN. 

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-25-08-One-Two-Three-Four/3.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Setting aside what it isn't, let's look at what it is. I took a course CS553-Cryptography, being offered by [<u>Dr. Dhiman Saha</u>](https://dhimans.in/), who is a fascinating individual deeply passionate about crypto(graphy, for those thinking about cryptocurrency). I've been meaning to maintain an account of this course on a day-to-day basis. My procrastinator monkey convinced me that weekly blogs are sufficient for the course. Now, we're 6 lectures down, not a single blog out yet and so here I am grouping One, Two, Three, and Four while still convincing myself that I'll definitely be more regular next class onwards.

Ugghhh... Let's do this!

#### One

Defense Against the Dark Arts! That's what the lecture started with. An analogy between crypto and the magical dark arts. If that wasn't enough, slide no. 2 had... why don't you guess it? Hint: It had Benedict Cumberbatch in it. Dreamy, right? Well, not for long. Turns out that **you can fail this course**. Turns out that **crypto is hard**. And our instructor spared no expense in making this clear. 

Mixed emotions in the audience, he introduced crypto as the story of Alice and Bob, 2 lovers always trying to exchange secrets. Then the bad guy, Eve. (There's always a bad guy!) What are the goals of cryptography? There's the notion of privacy; you don't want Eve to read Alice's message to Bob. There's also the notion of integrity; you don't want Eve to tamper with Alice's message to Bob. And there's authenticity. You don't want Eve to impersonate Alice while communicating with Bob. There are a bunch of other goals including authorization but this course shall focus on these three goals.

Alice, Bob, and Eve aside, we saw the various mechanisms being employed to achieve these cryptographic goals on a simple *http**s*** response from [https://google.com](https://google.com). 
- TLS: Transport Layer Security : Privacy of information
- ECDHE: Elliptic Curve Diffie Hellman: Key Exchange Mechanism
- ECDSA: Elliptic Curve Digital Signature Algorithm 
- AES: Privacy
- SHA256

At this point, we were introduced to Kerchoff's principle. "Everything about a cryptosystem except the key is public knowledge", he said (or wrote). Okay! Fine! He probably wrote it in French. Then we discussed an ancient, yet definitely uncool, cipher: The Shift Cipher. Don't see a point in putting it here but it'd just be cool to know that Caesar used a shift of 3. I remember promising myself that I'd read up more about modular arithmetic. Of course, I didn't, then at least. 

- Cryptology
    - Cryptography
        - Symmetric
            - Block
            - Stream
            - Hash
            - MACs
        - Asymmetric
            - Integer Factorization
            - Discrete Log
            - Digital Signatures
        - Protocols
    - Cryptanalysis
        - Social Engineering
        - Implementation Based
            - Power Analysis
        - Classical
            - Mathematical
            - Brute-Force

#### Two

First week of classes, the middle of the week, Wednesday. 
Class started with a classification of ciphers using something like a Venn diagram. Here are some of the categories: Simple substitution, key addition, polyalphabetic substitution, homophonic substitution, codebook (the Japs used this in WWII), and transposition. Then came a cool timeline of how cryptography has evolved over centuries. 

At this point, we formally defined a cryptosystem. A five-tuple is all we need: *P, C, K, E, D*.

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-25-08-One-Two-Three-Four/1.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Encryption functions must be injective. The decryption function must always be deterministic whereas the encryption function may be deterministic/probabilistic. What are the notions of security and efficiency in crypto?

We learned about the indistinguishability game while trying to understand the notion of semantic security. Semantic security suggests that a given ciphertext should leak no information about the plaintext to which it belongs. The indistinguishability game takes a pair of plaintext messages and passes them to an oracle which encrypts the messages. An adversary, given both plaintext and ciphertexts, attempts to map each one to its counterpart. If his probability of success is greater than 50% then the cryptosystem is insecure.

At this point, we got our hands dirty with a bit of math. We learned about groups and rings. A well-known ring is {Z, +, *}. But then we thought about the ring, {Z_m, +, *}. What's so special right? Well, there's an entire branch of mathematics to deal with this kinda stuff. Cool kids call it **Modulo Arithmetic**. Remember, I thought of reading up about this, right? Well, I didn't and I promised myself to read up, **AGAIN**. 
FYI: I Didn't, again,

The class closed with another cool historical cipher: The Affine Cipher. Affine <- Affinity <- *Affinis* (Latin). Well, in Euclidean Geometry, the Affine transformation refers to transformations that preserve lines and parallelism but not necessarily distances and length. 

#### Three

Friday's class got canceled. Yaaaaay! Right? Well, there was a makeup lecture on a Saturday morning later.
Anyways, we saw the Venn(-like) diagram classifying cipher, again. Here it is:

We then studied historical ciphers like the Vigenere cipher, Hill cipher, and Transposition cipher. Thought about how the transposition cipher is a particular case of the Hill cipher.

Then we came to attack models. They're classified as follows:
- Black Box
    - Ciphertext Only Attax
    - Known Plaintext Attax
        - KPA Attack on PKZip
        - Hill?
    - Chosen Plaintext Attax
        - Affine?
    - Chosen Ciphertext Attax
    - Adaptively Chosen Ciphertext Attax
- Grey Box
- White Box

Black Box models give the adversary the least power. They only allow query-level access. The level of access differs, giving increasing power to the adversary from COA to A-CCA. 
Grey box models provide Eve with access to the implementation of the cipher. This leads to a whole range of attacks ranging from side-channel attacks to software/hardware, and invasive/non-invasive attacks.
The white box gives you everything. Literally. Like the key is embedded within the public code available to Eve. Obfuscated, of course, yet known for sure.

Formal definitions were provided for KPA and CPA.
* Given one or more plaintexts and their corresponding ciphertexts, if it is very difficult to obtain the plaintext corresponding to a ciphertext not already known, the system is said to be KPA secure.
* For any list of plaintexts m1,m2,··· ,mn ∈ P chosen by the adversary, even with knowledge of the corresponding ciphertexts eK (m1), eK (m2), · · · , eK (mn) it is very difficult to decrypt any ciphertext c that is not in the given list without knowing k. (CPA secure)

We were asked to write a definition for CCA security. Here is my horrible attempt that badly needs to be redone:
* If given any set of (plaintext, ciphertext) 2-tuples, it is very difficult to obtain the plaintext corresponding to a ciphertext, not in the above-given set, the system is said to be CCA secure.

#### Four

This one started with an image of Claude Shannon and his paper titled "Communication Theory of Secrecy Systems". Since this blog is coming 3 lectures after it was actually supposed to, I know that Massey's interpretation of this paper actually holds a lot of weight when thinking about block ciphers. But that's a headache for another day.

Cryptographic security isn't the same as the definitions we have for computer security. In cryptography, well-defined problems are tried to be made hard to solve. *Impossibility* of a capable attacker exploiting a cipher's security can be defined in one of two ways: Practically (Computational Security) and Theoretically (Information Security)

Theoretical notions of security are binary, i.e. a cipher is secure or insecure. Practical notions provide a framework for quantifying the strength of a cipher. Computer security is generally defined in terms of 2 values:
- t, the lower bound on the number of operations that can be carried out by an adversary
- ε (read Epsilon), is a lower bound on the probability of success of an attack carried out by the above adversary

     “A crypto-scheme is (t, ε) − secure if every adversary performing at most t operations succeeds in breaking the scheme with probability at most ε”

Time for another tree:

Cryptographic Security
- Provable Security
    - Relative to a Mathematical Problem
        - Public Key Ciphers
        - eg. Integer Factorization
    - Relative to a Crypto Problem
        - Symmetric Key Ciphers
- Heuristic Security
    - Not provably, but probably secure
    - Believed to be secure
    - Due to the absence of attacks after extensive cryptanalysis
    - Notion of Security Margin
    - Round-reduced / Simplified Version Cryptanalysis

Next came the discussion on the informational theory aspect of a cipher's security. 

    A cipher is informationally secure only if, even given unlimited computation time and memory, it cannot be broken.

The lecture closed with a lemma on **perfect secrecy**. But what is it?
> A cryptosystem has perfect secrecy if **Pr**[x|y] = **Pr**[x] for all x ∈ P,y ∈ C.

Simple as that, innit? Try proving this then...

    Suppose (P, C, K, E, D) is a cryptosystem where |K| = |P| = |C|, then the cryptosystem provides perfect secrecy 
    if and only if every key is used with equal probability 1/|K|, and for every x ∈ P and y ∈ C there is a unique 
    K such that eK(x) = y.

#### CTF

Time for our first assignment. The instructor wasn't letting us off easily on this one trust me. He got the idea to set our assignment as the flag to capture and whichever team found this first would get a bonus. **GAME ON**.

Posted the assignment at 11:45 PM on Saturday night and we were waiting for it in the CC Lab (B109). We opened it, and the *.txt* encoded document had gibberish and we were shocked. It was a few minutes till we realized that it wasn't only the text file that was shared with us.

Apparently, we had a shift cipher on our hands. Cool! Easy right? Well, NO! Still had to code the decryption function. I got started and it was irritating as crap to write a seemingly simple piece of code. PRESSSSSUUUUURRREEE. Notebooks and pens and a lot of meaningless scribbling later, one of us came up with the idea to find the code online. Why didn't I think of this earlier??!! We found a python script. But it was working only over a field of 26 characters. All characters were encoded and decoded into capital Alphabet. A lot of ASCII characters were absent. The changes made seem simple now but god knows how much we racked our brains. It goes to the point that it is embarrassing to think of right now.

Once the code was running, we didn't know what to look for. Chaitanya was silently playing about with his own code and casually mentioned that he saw something like a "drive.google.com" somewhere in the output but it must have been a mistake or a coincidence. With that in the back of my mind, I was gazing at the plaintext output, lost in my own thoughts. Then it flashed, "drive.google.com/..." Terminated the running process immediately and pasted the drive link that I found. Jo rona aaya na boss, can't wish something like this on my worst enemy. Yet someone was doing this to us. This is what we found:

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-25-08-One-Two-Three-Four/gif1.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Restarted my script and kept looking. Passed through the old link and the key kept incrementing (I terminated the loop at 94 since that was as many characters in the field of the cipher). Found another drive link. Half expecting a hit and a fail, I opened it. GOOOOODDDD! Where are YOU! This is what I found. At least now I know what my worst enemy deserves. A CTF!

This is what showed up in the link:

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-25-08-One-Two-Three-Four/gif2.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Restarted my script and decided not to terminate it until it ends on its own. Upon scrolling through the deciphered text, I found another drive link. The third time's the charm indeed. Here's the [<u>link</u>](/assets/pdf/) to the assignment we got. That wasn't any less hectic, trust me. We submitted it an hour before the deadline, nothing to be proud of. But IG we shouldn't expect anything less from Dhiman sir.

#### Notes

Been a hectic few weeks. What with coursework, GSoC, and OpenLake to handle College life sucks from where I'm right now. Just need some time to chill. Not that I am not chilling. But chilling during vacations is a different thing altogether. Got to scribe Lecture 5 of CS553. Will prolly make that a blog post on its own. And yeah, we won the CTF. BitBees stood first and we got 10 bonus points, *if we turned in a decent enough assignment that didn't eat up the edge we got*. 

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-25-08-One-Two-Three-Four/2.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Cheers to us! Let's see how we do!
