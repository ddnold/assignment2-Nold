# Dustin Nold
---
I was born in Austin, Texas on May 20th, 2000. I enjoy playing video games sometimes, I mostly just enjoy computers as a whole though. My dad has been in the military until very recently. As a result of this my childhood was spread thinly throughout the United States, at one point I even lived in Alaska. However by highschool I had moved in with my grandma and ended up settling down in Saint Joseph. I had heard a bunch about how NW had a great cs program, and of course I heard about the party scene, so I decided to take my college experience this way. And that is the jist of how I got to typing this today. 

In other words, this is **[me](DustinNoldPic.jpg)**

---
The following table includes some sports. These are sports that I have either played or considered playing. I would suggest any sporty people look into these for potential play.

| Sport | Location | Cost |
| :---: | :---: | :---: |
| Baseball | Baseball Field | $200 - $400 |
| Football | Football Field | $200 - $500 |
| Soccer | Soccer Field | $200 - $500 |
| Tennis | Tennis Court | $200 - $1000 |

---
## Favorite Quotes

> Compare yourself to who you were yesterday, not to who someone else is today.

- *Jordan Peterson*

> When you have something to say, silence is a lie.

- *Jordan Peterson*

---
## Rabin-Karp Pattern Searching 
>> The following algorithim takes a string and a substring. It hashes the substring you are searching for and takes its length. It then hashes all the substrings of that length from the string and puts them into a table. From there it matches them and returns where the substrings appear in the string. More information can be found [here.](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)

[source code](https://cp-algorithms.com/string/rabin-karp.html)

```vector<int> rabin_karp(string const& s, string const& t) {
    const int p = 31; 
    const int m = 1e9 + 9;
    int S = s.size(), T = t.size();

    vector<long long> p_pow(max(S, T)); 
    p_pow[0] = 1; 
    for (int i = 1; i < (int)p_pow.size(); i++) 
        p_pow[i] = (p_pow[i-1] * p) % m;

    vector<long long> h(T + 1, 0); 
    for (int i = 0; i < T; i++)
        h[i+1] = (h[i] + (t[i] - 'a' + 1) * p_pow[i]) % m; 
    long long h_s = 0; 
    for (int i = 0; i < S; i++) 
        h_s = (h_s + (s[i] - 'a' + 1) * p_pow[i]) % m; 

    vector<int> occurences;
    for (int i = 0; i + S - 1 < T; i++) { 
        long long cur_h = (h[i+S] + m - h[i]) % m; 
        if (cur_h == h_s * p_pow[i] % m)
            occurences.push_back(i);
    }
    return occurences;
}
```

