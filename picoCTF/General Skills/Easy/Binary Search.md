# Author: Jeffery John
General Skills / Algorithms Objective: Guess a random number between 1 and 1000 in only 10 tries.

# Description
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses. Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools! You can download the challenge files here:

[challenge.zip](https://artifacts.picoctf.net/c_atlas/18/challenge.zip)

Additional details will be available after launching your challenge instance.

# Hints
1.  Have you ever played hot or cold? Binary search is a bit like that.
2.  You have a very limited number of guesses. Try larger jumps between numbers!
3.  The program will randomly choose a new number each time you connect. You can always try again, but you should start your binary search over from the beginning - try around 500. Can you think of why?

# The Core Concept: Divide and Conquer
**Note: I have to be honest here, I'd finished this room months ago but didn't write a writeup or learn anythin behind it so I take a chance to do here**

The "point" of this room is to demonstrate the efficiency of O(log n) algorithms compared to random guessing or linear searching.

In a normal "linear" search (like looking for a word in a dictionary by reading every single page from the start), you might have to check every single item. If the number is 1,000, you might need 1,000 guesses.

Binary Search works differently. Because the data is sorted (1 to 1000), you can eliminate half of the remaining possibilities with every single guess.

    The Math: 210=1024.

    This means that by splitting the range in half 10 times, you can mathematically isolate any specific number out of 1,024 possibilities. This is why the challenge gives you exactly 10 guesses for a range of 1000. It’s not random; it’s the exact mathematical limit needed for a perfect strategy.
    
# The Theory: Why "Binary Search"?
Before solving, it's important to understand why the limit is specifically 10 guesses. This isn't arbitrary—it's based on the Binary Search Algorithm.

If we guess randomly, our odds are terrible (1/1000). If we count up 1, 2, 3... (Linear Search), we will run out of turns. Binary Search is a strategy where we always guess the exact middle of the current range.

    If the range is 1–1000, we guess 500.

    If the target is "Lower", we instantly know the number is 1–499. We just deleted 500 wrong answers with one guess!

Since 210=1024, we can prove mathematically that 10 guesses are enough to find any number up to 1,024.

    Guess 1: 1000 options → 500

    Guess 2: 500 → 250

    Guess 3: 250 → 125

    ...

    Guess 10: 2 → 1 (The Answer)

# Steps
1. Connected to the challenge via SSH.
2. Once connected, I followed the halving strategy:

    Range: 1–1000. Guess: 500. (Feedback: Lower)

    Range: 1–499. Midpoint: 250. (Feedback: Higher)

    Range: 251–499. Midpoint: 375. (Feedback: Higher)

    Range: 376–499. Midpoint: 437. ... (Continue until the flag is revealed)

3. This challenge visualizes Time Complexity.

    Linear Search: O(n) (Linear time) — Takes up to 1,000 steps.

    Binary Search: O(logn) (Logarithmic time) — Takes roughly log2​(1000)≈10 steps.
   
*In cybersecurity, this concept is often used in Side-Channel Attacks (timing attacks) or blindly extracting database data (Blind SQL Injection), where you guess one bit of information at a time by asking "True/False" questions.*

# 💡 Pro Tip: The "Real World" Application

While this challenge feels like a simple guessing game, the Binary Search logic is actually the foundation of a critical web attack called Blind SQL Injection (Blind SQLi).

In a Blind SQLi scenario, the database doesn't show you any data; it only answers "True" or "False" (e.g., the page loads normally or it returns an error).

    The Problem: If you want to steal a password, you can't just "read" it. You have to guess it one letter at a time.

    The Wrong Way (Linear): "Is the first letter 'a'? Is it 'b'? Is it 'c'?" (This generates thousands of suspicious logs).

    The Right Way (Binary Search): "Is the ASCII value of the first letter greater than 100?"

        If Yes, you just eliminated 'a', 'b', 'c', and dozens of other characters in one request.

Takeaway: Mastering binary search isn't just about algorithms; it's about learning how to exfiltrate data efficiently when you have limited feedback from a target system.

Answer: picoCTF{g00d_gu355_2e90d29b}
