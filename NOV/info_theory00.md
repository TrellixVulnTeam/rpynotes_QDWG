
## Information Theory

- The field of information theory was developed in the 1940s by Claude Shannon, with the initial exposition reported in (Shannon 1948). 
- Shannon was interested in the problem of maximizing the amount of information that you can transmit over an imperfect communication channel such as a noisy phone line (though actually many of his concerns stemmed from codebreaking in World War II). 
- For any source of ‘information’ and any ‘communication channel,’ Shannon wanted to be able to determine theoretical maxima for (i) data compression - which turns out to be given by the Entropy H (or more fundamentally, by the Kolmogorov complexity K), and (ii) the transmission rate - which is given by the Channel Capacity C. 
- Until Shannon, people had assumed that necessarily, if you send your message at a higher speed, then more errors must occur during the transmission. But Shannon showed that providing that you transmit the information in your message at a slower rate than the Channel Capacity, then you can make the probability of errors in the transmission of your message as small as you would like.

### Entropy

- Let p(x) be the probability mass function of a random variable X, over a discrete set of symbols (or **alphabet**) $mathcal{X}$:
- $p(x)=P(X=x), x \in \mathcal{X}$
- For example, if we toss two coins and count the number of heads, we have a random variable: p(0)=1/4, p(1)=1/2, p(2)=1/4.
- The **entropy** (or **self-information**) is the average uncertainty of a single random variable:
$$ Entropy\text{ }H(p)=H(X)=-\sum_{x\in\mathcal{X}}p(x)log_2p(x) - - - -\dots(1)$$

- Entropy measures the amount of information in a random variable. 
- It is normally measured in bits (hence the log to the base 2), but using any other base yields only a linear scaling of results. 
- For the rest of this book, an unadorned log should be read as log to the base 2. 
- Also, for this definition to make sense, we define 0 log 0 = 0.

#### Example 1
Suppose you are reporting the result of rolling an g-sided die. Then the entropy is:

$$H(X)=-\sum_{i=1}^8p(i)log{p}(i)=-\sum_{i=1}^8\frac{1}{8}log{\frac{1}{8}}= -log{\frac{1}{8}}=log8=3 bits$$.

- This is what we would expect. Entropy, the amount of information in a random variable, can be thought of as the average length of the message needed to transmit an outcome of that variable. 
- If we wish to send the result of rolling an eight-sided die, the most efficient way is to simply encode the result as a 3 digit binary message:
$$\begin{matrix}1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 \\
001 & 010 & 011 & 100 & 101 & 110 & 111 & 000 \end{matrix}$$

- The transmission cost of each result is 3 bits, and there is no cleverer way of encoding the results with a lower average transmission cost. 
- In general, an optimal code sends a message of probability p(i) in I- log p(i) 1 bits.
- The minus sign at the start of the formula for entropy can be moved inside the logarithm, where it becomes a reciprocal
$$H(X)=\sum_{x\in\mathcal{X}}p(x)log{\frac{1}{p(x)}} - - - -\dots(2) $$

- People without any statistics background often think about a formula like this as a sum of the quantity p(x) log( l/ p(x)) for each x.
- While this is mathematically impeccable, it is the wrong way to think about such equations. Rather you should think of $\sum_{x\in\mathcal{X}}p(x)\dots$ as an idiom. 
- It says to take a weighted average of the rest of the formula (which will be a function of x), where the weighting depends on the probability of each x.
- Technically, this idiom defines an expectation, as we saw earlier. Indeed
$$H(X)=E\left(log\frac{1}{p(X)}\right) - - - -\dots(3)$$

#### Example 2: Simplified Polynesian
Simplified Polynesian (languages such as Hawai'ian known for small alphabets) appears to be just a random sequence of letters, with the letter frequencies as shown:
Then the per-letter entropy is:
$$\begin{aligned}H(P) &= - \sum_{i\in\{p,t,k,a,i,u\}}P(i)log{P(i)} \\
    &= -[4\times\frac{1}{8}log{\frac{1}{8}}+2\times\frac{1}{4}log{\frac{1}{4}}] \\
    &= 2\frac{1}{2} bits
\end{aligned}$$

- This is supported by the fact that we can design a code that on average takes $2\frac{1}{2}$ bits to transmit a letter:

$$\begin{matrix}p & t & k & a & i & u \\
100 & 00 & 101 & 01 & 110 & 111 \end{matrix}$$

- Note that this code has been designed so that fewer bits are used to send more frequent letters, but still so that it can be unambiguously decoded
- if a code starts with a 0 then it is of length two, and if it starts with a 1 it is of length 3. 
- There is much work in information theory on the design of such codes, but we will not further discuss them here.
- One can also think of entropy in terms of the Twenty Questions game.
- If you can ask yes/no questions like ‘Is it a t or an a?’ or ‘Is it a consonant?’ then on average you will need to ask $2\frac{1}{2}$ questions to identify each letter with total certainty (assuming that you ask good questions!).
- In other words, entropy can be interpreted as a measure of the size of the ‘search space’ consisting of the possible values of a random variable and its associated probabilities.
- Note that: (i) $H(X)\ge 0$, (ii) H(X) = 0 only when the value of X is determinate, hence providing no new information, and that (iii) entropy increases with the message length. 
- The information needed to transmit the results of tossing a possibly weighted coin depends on the probability p that it comes up heads, and on the number of tosses made. 
- The entropy for a single toss is shown in figure 1. 
- For multiple tosses, since each is independent, we would just multiply the number in the graph by the number of tosses.
![Figure 1](https://selene.hud.ac.uk/u1273400/images/seg_media/ent0.PNG)
**Figure 1**:Theentropy of a weighted coin. The horizontal axis shows the probability of a weighted coin to come up heads. The vertical axis shows the entropy of tossing the corresponding coin once

### Joint entropy and conditional entropy
- The joint entropy of a pair of discrete random variables X, Y ~p(x,y) is the amount of information needed on average to specify both their values. It is defined as
$$ H(X,Y)=-\sum_{x\in\mathcal{X}}\sum_{y\in\mathcal{Y}}p(x,y)log{p(x,y)} - - - -\dots(4)$$
- The conditional entropy of a discrete random variable Y given another X, for X, Y - p(x, y), expresses how much extra information you still need to supply on average to communicate Y given that the other party knows X:
$$\begin{aligned}H(Y|X) &=\sum_{x\in\mathcal{X}}p(x)H(Y|X=x) \\
    &= \sum_{x\in\mathcal{X}}p(x)\left[-sum_{y\in\mathcal{Y}}log{p(y|x)}\right] \\
    &= -\sum_{x\in\mathcal{X}}\sum_{y\in\mathcal{Y}}p(x,y)log{p(y|x)}
\end{aligned} - - - -\dots(5)$$
There is also a chain rule for entropy:
$$\begin{aligned}H(X,Y) &= H(X)+H(Y|X) \\
    H(X_1,\dots,X_n) &= H(X)+H(X_2|X_1)+\dots+H(X_n|X_1,\dots,X_{n-1}
\end{aligned} - - - -\dots(6)$$

- The products in the chain rules for probabilities here become sums because of the log
$$\begin{aligned} H(X,Y) &= -E_{p(x,y)}(log{p}(x,y)) \\
    &= -E_{p(x,y)}(log{p}(x)p(y|x))) \\
    &= -E_{p(x,y)}(log{p}(x)+log{p}(y|x))) \\
    &= -E_{p(x,y)}(log{p}(x))-E_{p(x,y)}(log{p}(y|x)) \\
    &= H(X)+H(Y|X)
\end{aligned}$$

#### Example 3: Simplified Polynesian Revisited
- An important scientific idea is the distinction between a model and reality. Simplified Polynesian isn’t a random variable, but we approximated it (or modeled it) as one. But now let’s learn a bit more about the language. Further fieldwork has revealed that Simplified Polynesian has syllable structure. Indeed, it turns out that all words consist of sequences of CV (consonant-vowel) syllables. This suggests a better model in terms of two random variables C for the consonant of a syllable, and V for the vowel, whose joint distribution P(C, V) and marginal distributions P( C, .) and P(. , V) are as follows:
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l"></th>
    <th class="tg-yw4l">p</th>
    <th class="tg-yw4l">t</th>
    <th class="tg-yw4l">k</th>
    <th class="tg-yw4l"></th>
  </tr>
  <tr>
    <td class="tg-yw4l">a</td>
    <td class="tg-yw4l">$\frac{1}{16}$</td>
    <td class="tg-yw4l">$\frac{3}{8}$</td>
    <td class="tg-yw4l">$\frac{1}{16}$</td>
    <td class="tg-yw4l">$\frac{1}{2}$</td>
  </tr>
  <tr>
    <td class="tg-yw4l">i</td>
    <td class="tg-yw4l">$\frac{1}{16}$</td>
    <td class="tg-yw4l">$\frac{3}{16}$</td>
    <td class="tg-yw4l">0</td>
    <td class="tg-yw4l">$\frac{1}{4}$</td>
  </tr>
  <tr>
    <td class="tg-yw4l">u</td>
    <td class="tg-yw4l">0</td>
    <td class="tg-yw4l">$\frac{3}{16}$</td>
    <td class="tg-yw4l">$\frac{1}{16}$</td>
    <td class="tg-yw4l">$\frac{1}{4}$</td>
  </tr>
  <tr>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">$\frac{1}{8}$</td>
    <td class="tg-yw4l">$\frac{3}{4}$</td>
    <td class="tg-yw4l">$\frac{1}{16}$</td>
    <td class="tg-yw4l"></td>
  </tr>
</table>

- Note that here the marginal probabilities are on a per-syllable basis, and are therefore double the probabilities of the letters on a per-letter basis, which would be:
$$\begin{matrix}p & t & k & a & i & u \\
1/16 & 3/8 & 1/16 & 1/4 & 1/8 & 1/8 \end{matrix}$$

##### Solution

- We can work out the entropy of the joint distribution, in more than one way.  Let us use the chain rule.
- Within the calculation, we use an informal, but convenient, notation of expressing a finite-valued distribution as a sequence of probabilities, which we can calculate the entropy of.

$$\begin{aligned}H(C) &= 2 \times \frac{1}{8} \times 3 + \frac{3}{4}(2-log{3}) \\
    &= \frac{9}{4}-\frac{3}{4}log{3}\text{ bits }\approx 1.061 bits
\end{aligned}$$
$$\begin{aligned}H(V|C) &= \sum_{c=p,t,k}p(\mathcal{C}=c)H(V|\mathcal{C}=c) \\
    &= \frac{1}{8}H\left(\frac{1}{2},\frac{1}{2},0\right)-\frac{3}{4}H\left(\frac{1}{2},\frac{1}{4},\frac{1}{4}\right)+\frac{1}{8}H\left(\frac{1}{2},0\frac{1}{2}\right) \\
    &= 2\times\frac{1}{8}\times 1+\frac{3}{4}\left[\frac{1}{2}\times 1+2\times\frac{1}{4}\times 2\right] \\
    &= \frac{1}{4} + \frac{3}{4} \times \frac{3}{2} \\
    &= \frac{11}{8} bits = 1.375 bits
\end{aligned}$$
$$\begin{aligned}H(C,V) &=H(C)+H(V|C) \\
    &= \frac{9}{4}-\frac{3}{4}log{3}+\frac{11}{8} \\
    &= \frac{29}{8}-\frac{3}{4}log{3}\text{ bits }\approx 2.44 bits
\end{aligned}$$

- Note that those 2.44 bits are now the entropy for a whole syllable (which was $2 x 2\frac{1}{2} = 5$ for the original Simplified Polynesian example). 
- Our better understanding of the language means that we are now much less uncertain, and hence less surprised by what we see on average than before.
- Because the amount of information contained in a message depends on the length of the message, we normally want to talk in terms of the perletter or per-word entropy. 
- For a message of length n, the per-letter/word entropy, also known as the entropy rate, is:
$$H_{rate}=\frac{1}{n}H(X_{1n})=-\frac{1}{n}\sum_{x_{1n}}(x_{1n})log{p}(x_{1n}) - - - -\dots(7)$$

- If we then assume that a language is a stochastic process consisting of a sequence of tokens $L=(Xi)$, for example a transcription of every word you utter in your life, or a corpus comprising everything that is sent down the newswire to your local paper, then we can define the entropy of a human language L as the entropy rate for that stochastic process:
$$H_{rate}(L)=\lim_{n\rightarrow\infty}\frac{1}{n}H(X_1,X_2,\dots,X_n)- - - -\dots(8)$$
- We take the entropy rate of a language to be the limit of the entropy rate of a sample of the language as the sample gets longer and longer.

### Mutual information
By the chain rule for entropy,
$$H(X,Y)=H(X)+H(Y|X)=H(Y)+H(X|Y)$$
Therefore
$$H(X)-H(X|Y)=H(Y)-H(Y|X)$$

- This difference is called the mutual information between X and Y. 
- It is the reduction in uncertainty of one random variable due to knowing about another, or in other words, the amount of information one random variable contains about another. 
- A diagram illustrating the definition of mutual information and its relationship to entropy is shown in figure 2.
![Figure 2](https://selene.hud.ac.uk/u1273400/images/seg_media/ent1.PNG)
**Figure 2**:The relationship between mutual information I and entropy H.

- Mutual information is a symmetric, non-negative measure of the common information in the two variables. People thus often think of mutual information as a measure of dependence between variables. However, it is actually better to think of it as a measure of independence because:
- It is 0 only when two variables are independent, but
- For two dependent variables, mutual information grows not only with the degree of dependence, but also according to the entropy of the variables.
- Simple arithmetic gives us the following formulas for mutual information I(X;Y):
$$\begin{aligned}I(X;Y) &=H(X)-H(X|Y) \\
    &= H(X)+H(Y)-H(X,Y) \\
    &= \sum_{x}P(x)log\frac{1}{p(x)}+\sum_yp(y)log\frac{1}{p(y)}+\sum_{x,y}p(x,y)log{p}(x,y) \\
    &= \sum_{x,y}log\frac{p(x,y)}{p(x)p(y)}
\end{aligned}- -(9)$$

- Since H(X|X)=0 Note that H(X)=H(X)-H(X|X)=I(X;X)

- This illustrates both why entropy is also called self-information, and how the mutual information between two totally dependent variables is not constant but depends on their entropy.
- We can also derive conditional mutual information and a chain rule:
$$ I(X;Y|Z)=I(X;Y|Z)=H(X|Z)-H((X|Y,Z) - - - -\dots(10)$$
$$\begin{aligned}I(X_{1n};Y) &=I(X_1;Y)+\dots+ I(X_n;Y|X_1,\dots,X_{n-1}) \\
    &= \sum_{i=1}^nI(X_i;Y|X_1,\dots,X_{n-1})
\end{aligned}- -(11)$$

- In this section we have defined the mutual information between two  random variables. Sometimes people talk about the **pointwise mutual information** between two particular points in those distributions
$$I(x,y)=log\frac{p(x,Y)}{p(x)P(Y)}$$

- This has sometimes been used as a measure of association between elements, but there are problems with using this measure
- Mutual information has been used many times in Statistical NLP, such as for clustering words 
- It also turns up in word sense disambiguation.

### The noisy channel
- Using information theory, Shannon modeled the goal of communicating down a telephone line - or in general across any channel - in the following way: 
- The aim is to optimize in terms of throughput and accuracy the communication of messages in the presence of noise in the channel. 
- It is assumed that the output of the channel depends probabilistically on  the input.
- In general, there is a duality between **compression**, which is achieved by removing all redundancy, and transmission accuracy, which is achieved by adding controlled **redundancy** so that the input can be recovered even in the presence of noise. 
- The goal is to encode the message in such a way that it occupies minimal space while still containing enough redundancy to be able to detect and correct errors. 
- On receipt, the message is then decoded to give what was most likely the original message. This process is shown in figure 3.
![Figure 3](https://selene.hud.ac.uk/u1273400/images/seg_media/ent2.PNG)
**Figure 3**: The noisy channel model


- The central concept that characterizes a channel in information theory is its **capacity**. 
- The channel capacity describes the rate at which one can transmit information through the channel with an arbitrarily low probability of being unable to recover the input from the output. 
- For a memoryless channel, Shannon’s second theorem states that the channel capacity can be determined in terms of mutual information as follow
$$ C=max_{p(X)}I(X;Y) - - - -\dots(13)$$

- According to this definition, we reach a channel’s capacity if we manage to design an input code X whose distribution maximizes the mutual information between the input and the output over all possible input distributions p(X).
- As an example, consider the binary symmetric channel in figure 4.
![Figure 4](https://selene.hud.ac.uk/u1273400/images/seg_media/ent3.PNG)
**Figure 4** A binary symmetric channel. A 1 or a 0 in the input gets flipped on trasnsmission with probability p

- Each input symbol is either a 1 or a 0, and noise in the channel causes each symbol to be flipped in the output with probability p. We find that
$$ I(X;Y)=H(Y)-H(Y|X) = H(Y)-H(p)$$

Therefore
$$max_{p(X)}I(X;Y)=1-H(p)$$

- This last line follows because the mutual information is maximized by maximizing the entropy in the codes, which is done by making the input and hence the output distribution uniform, so their entropy is 1 bit.
- Since entropy is non-negative, $C \le 1$. 
- The channel capacity is 1 bit only if the entropy is zero, that is if p = 0 and the channel reliably transmits a 0 as 0 and a 1 as 1, or if p = 1 and it always flips bits. 
- A completely noisy binary channel which transmits both OS and 1s with equal probability as OS and 1s (i.e., p = i) has capacity C = 0, since in this case there is no mutual information between X and Y.
- Such a channel is useless for communication.
- It was one of the early triumphs of information theory that Shannon was able to show two important properties of channels. 
- First, channel capacity is a well-defined notion. In other words, for each channel there is a smallest upper bound of I(X; Y) over possible distributions p(X).
- Second, in many practical applications it is easy to get close to the optimal channel capacity.
- We can design a code appropriate for the channel that will transmit information at a rate that is optimal or very close to optimal.
- The concept of capacity eliminates a good part of the guesswork that was involved in designing communications systems before Shannon.
- One can precisely evaluate how good a code is for a communication line and design systems with optimal or near-optimal performance.
- The noisy channel model is important in Statistical NLP because a simplified version of it was at the heart of the renaissance of quantitative natural language processing in the 1970s. 
- In the first large quantitative project after the early quantitative NLP work in the 1950s and 60s researchers at IBM’s T. J. Watson research center cast both speech recognition and machine translation as a noisy channel problem.
- Doing linguistics via the noisy channel model, we do not get to control the encoding phase. We simply want to decode the output to give the most likely input, and so we work with the channel shown in figure 5. 
![Figure 5](https://selene.hud.ac.uk/u1273400/images/seg_media/ent4.PNG)

- Many problems in NLP can be construed as an attempt to determine the most likely input given a certain output. 
- We can determine this as follows, by using Bayes' theorem, and then noting that the output probability is constant:
$$ \hat{I}=argmax_Ip(i|o)=argmax_I\frac{p(i)p(o|i)}{p(o)}=argmax_Ip(i)p(o|i) - - - - \dots(14)$$

- Here we have two probability distributions to consider: p(i) is the **language model**, the distribution of sequences of ‘words’ in the input language, and p(o|i) is the **channel probability**.
- As an example, suppose we want to translate a text from English to French. The noisy channel model for translation assumes that the true text is in French, but that, unfortunately, when it was transmitted to us, it went through a noisy communication channel and came out as English.
- So the word cow we see in the text was really vuche, garbled by the noisy channel to cow. 
- All we need to do in order to translate is to recover the original French - or to decode the English to get the French.
- The validity of the noisy channel model for translation is still giving rise to many a heated debate among NLP researchers, but there is no doubt that it is an elegant mathematical framework that has inspired a significant amount of important research. 
- Other problems in Statistical NLP can also be seen as instantiations of the decoding problem. A selection is shown in table 1.
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l">Application</th>
    <th class="tg-yw4l">Input</th>
    <th class="tg-yw4l">Output</th>
    <th class="tg-yw4l">p(i)</th>
    <th class="tg-yw4l">p(o|i)</th>
  </tr>
  <tr>
    <td class="tg-yw4l">Machine Translation</td>
    <td class="tg-yw4l">$L_1$ word sequences</td>
    <td class="tg-yw4l">$L_2$ word sequences</td>
    <td class="tg-yw4l">$p(L_1)$ in a language model</td>
    <td class="tg-yw4l">translation model</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Optical Character recognition</td>
    <td class="tg-yw4l">actual text</td>
    <td class="tg-yw4l">text with mistakes</td>
    <td class="tg-yw4l">prob of language text</td>
    <td class="tg-yw4l">model of OCR errors</td>
  </tr>
  <tr>
    <td class="tg-yw4l">POS tagging</td>
    <td class="tg-yw4l">POS tag sequences</td>
    <td class="tg-yw4l">English words</td>
    <td class="tg-yw4l">Prob of POS sequences</td>
    <td class="tg-yw4l">p(w|t)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Speech Recognition</td>
    <td class="tg-yw4l">word sequences</td>
    <td class="tg-yw4l">speech signal</td>
    <td class="tg-yw4l">prob of word sequences</td>
    <td class="tg-yw4l">acoustic model</td>
  </tr>
</table>
**Table 1**: Statistical NLP problems as decoding problems.


### Relative entropy (Kullback-Leiber divergence)
For two probability mass functions, p(x), q(x) their relative entropy is given by:
$$D(p||q)=\sum_{x\in\mathcal{X}}p(x)log\frac{p(x)}{q(x)} - - - -\dots(15)$$
where again we define $0 log\frac{0}{q}=0$ and otherwise $p log\frac{p}{0}=\infty$.  The relative entropy, also known as the **Kullback-Leiber divergence**, is the measure of how different two probability distributions (over the same event space) are.  Expressed as an expectation we have.
$$D(p||q)=E_p\left(log\frac{p(X)}{q(X)}\right) - - - -\dots(16)$$



- Thus, the KL divergence between p and q is the average number of bits that are wasted by encoding events from a distribution p with a code based on a not-quite-right distribution q.
- This quantity is always non-negative, and D(p||q) = 0 iff p = q. For these reasons, some authors use the name ‘KL distance,’ but note that relative entropy is not a metric (in the sense in which the term is used in mathematics): it is not symmetric in p and q (see exercise 2.12), and it does not satisfy the triangle inequality.
- The triangle inequality is that for any three pints X, y, Z:$d(x,y)\le d(x,z)+d(z,y)$
- Hence we will use the name ‘KL divergence,’ but nevertheless, informally, people often think about the relative entropy as the ‘distance’ between two probability distributions: it gives us a measure of how close two pmfs are.
- Mutual information is actually just a measure of how far a joint distribution is from independence 
$$I(X; Y)=D(p(x,y)||p(x)p(y) - - - -\dots(17)$$

- We can also derive conditional relative entropy and a chain rule for relative entropy:
$$D(p(y|x)||q(y|x))=\sum_xp(x)\sum_yp(y|x)log\frac{p(x)}{q(x)} - - - -\dots(18)$$

$$D(p(y|x)||q(y|x))=D(p(x)||q(x)+D(p(y|x)||q(y|x) - - - -\dots(19)$$

### Cross Entropy
- So far we have examined the notion of entropy, and seen roughly how it is a guide to determining efficient codes for sending messages, but how does this relate to understanding language?
- The secret to this is to return to the idea that entropy is a measure of our uncertainty. 
- The more we know about something, the lower the entropy will be because we are less surprised by the outcome of a trial.
- We can illustrate this with the examples used above. Consider again Simplified Polynesian from examples 8 and 9. This language has 6 letters.
- The simplest code is to use 3 bits for each letter of the language.
- This is equivalent to assuming that a good model of the language (where our ‘model’ is simply a probability distribution) is a uniform model. 
- However, we noticed that not all the letters occurred equally often, and, noting these frequencies, produced a zeroth order model of the language. 
- This had a lower entropy of 2.5 bits per letter (and we showed how this observation could be used to produce a more efficient code for transmitting the language). 
- Thereafter, we noticed the syllable structure of the language, and developed an even better model that incorporated that syllable structure into it. 
- The resulting model had an even lower entropy of 1.22 bits per letter. The essential point here is that if a model captures more of the structure of a language, then the entropy of the model should be lower.
- In other words, we can use entropy as a measure of the quality of our models.
- Alternately, we can think of entropy as a matter of how surprised we will be. - Suppose that we are trying to predict the next word in a Simplified Polynesian text. That is, we are examining P(w I h), where w is the next word and h is the history of words seen so far. 
- A measure of our **surprise** on seeing the next word can be derived in terms of the conditional probability assigned to w by our model m of the distribution of Simplified Polynesian words.
- Surprise can be measured by what we might term the **pointwise entropy** $H(w|h) = -log_2 m(w|h)$. 
- If the predictor is certain that word w follows a given history h and it is correct, then the information supplied to the predictor on seeing w is $- log_2 1 = 0$. 
- In other words, the predictor does not experience any surprise at all. On the other hand, if the model thinks that w cannot follow h, then m(w|h) = 0 and so the information supplied to the predictor is infinite $(-log_2 0 = \infty$. 
- In this case our model is infinitely surprised, which is normally a very bad thing. 
- Usually our models will predict a probability between these two extremes for each event and so the model will gain some information, or alternatively, be somewhat surprised, when it sees the next word, and the goal is to keep that level of surprise as low as possible. 
- Summing over the surprise of the predictor at each word gives an expression for our total surprise:
$$\begin{aligned}H_{total}&=\sum_{j=1}^nlog_2m(w_j|w_1,w_2,\dots,w_{j-1}) \\
    &=-log_2 m(w_1,w_2,\dots,w_n) \end{aligned} $$

- The second line above follows from the chain rule. 
- Normally, we would want to normalize this measure by the length of the text so our notion of surprise is not dependent on the size of the text. 
- This normalized measure gives the average surprise of the predictor per word.
- So far this discussion has been rather informal, but we can formalize it through the notion of relative entropy. Suppose that we have some empirical phenomenon, in Statistical NLP usually utterances in a certain language.
- Assuming some mapping to numbers, we can represent it via a random variable X.
- Then we assume that there is some probability distribution over the utterances - for instance, you hear Thank you much more often than On you.
- So we take X ~ p(x).
- Now, unfortunately we do not know what p(.) is for empirical phenomena.
- But by looking at instances, for example by looking at a corpus of utterances, we can estimate roughly what p seems to be like. 
- In other words, we can produce a model m of the real distribution, based on our best estimates.
- In making this model, what we want to do is to minimize D(p||m) - to have as accurate a probabilistic model as possible.
- Unfortunately, we normally cannot calculate this relative entropy - again, because we do not know what p is.
- However, there is a related quantity, the cross entropy, which we fortunately can get a handle on.
- The **cross entropy** between a random variable X with true probability distribution p(x) and another pmf q (normally a model of p) is given by:
$$\begin{aligned}H(X,q) &= H(X)+D(p||q) - - - -\dots(20)\\
    &=-\sum_xp(x)log q(x) \\
    &=E_p\left(log\frac{1}{q(x)}\right) - - - -\dots(21) \end{aligned}$$

- Just as we previously defined the entropy of a language, we can also define the cross entropy of a langauge $L=(X_i)~p(x)$ according to a model m by:
$$H(L,m)=-lim_{n\rightarrow\infty}\frac{1}{n}\sum_{x_{1n}}p(x_{1n})log{m(x_{1n})} - - - -\dots(22)$$

- We do not seem to be making much progress, because it still sees that we cannot calculate this quantity without knowing p. but if we make certaina assumptions that the language is 'nice' then cross entropy for the language can be calculated as:
$$H(L,m)-lim_{n\rightarrow\infty}\frac{1}{n}\sum_{x_{1n}}p(x_{1n})log{m}(x_{1n}) - - - -\dots(23) $$
- Using this second form, we can calculate the cross entropy based only on knowing our probability model and having a large body of utterances available.  That is, we do not actually attempt to calculate the limit, but approximate it by calculating for a sufficiently large n:
$$H(L,m)\approx-\frac{1}{n}log{m}(x_{1n}) - - - -\dots(24)$$

- This measure is just the figure for our average surprise. Our goal will be to try to minimize this number. 
- Because H(X) is fixed (if unknown), this is equivalent to minimizing the relative entropy, which is a measure of how much our probability distribution departs from actual language use. 
- The only additional requirement is that the text that we use to test the model must be an independent test set, and not part of the training corpus that we used to estimate the parameters of the model. 
- Cross entropy is inversely related to the average probability a model assigns to words in test data.
- Lower model cross entropy normally leads to better performance in applications, but it need not do so if it is just a matter of improving the magnitude of probability estimates, but not their relative ordering.
- But what justifies going from equation (22) to equation (23)? 
- The formula for language cross entropy has an expectation embedded within it
$$H(L,m)=lim_{n\rightarrow\infty}\frac{1}{n}E\left(log\frac{1}{m(X_{1n})}\right) - - - -\dots(25)$$

- Recall that the expectation is a weighted average over all possible sequences. But in the above formula we are using a limit and looking at longer and longer sequences of language use. 
- Intuitively, the idea is then that if we have seen a huge amount of the language, what we have seen is ‘typical.’
- We no longer need to average over all samples of the language; the value for the entropy rate given by this particular sample will be roughly right.
- The formal version of this is to say that if we assume that $L = (X_i)$ is a stationary ergodic process, then we can prove the above result. 
- This is a consequence of the Shannon-McMillan-Breiman theorem, also known as the Asymptotic Equipartition Property:
- **Theorem**:  If $H_{rate}$ is the entropy rate of a finite-valued stationary ergodic process ($X_n$), then:
$$-\frac{1}{n}log{p}(X_1,\dots,X_n)\rightarrow H,\text{ with probability 1}$$

- An **ergodic** process is one that, roughly, cannot get into different substates that it will not escape from. 
- An example of a non-ergodic process is one that in the beginning chooses one of two states: one in which it generates 0 forever, one in which it generates 1 forever. 
- If a process is not ergodic, then even looking at one very long sequence will not necessarily tell us what its typical behavior is (for example, what is likely to happen when it gets restarted).
- A stationary process is one that does not change over time. 
- This is clearly wrong for language: new expressions regularly enter the language while others die out. 
- And so, it is not exactly correct to use this result to allow the calculation of a value for cross entropy for language applications.
- Nevertheless, for a snapshot of text from a certain period (such as one year’s newswire), we can assume that the language is near enough to unchanging, and so this is an acceptable approximation to truth. 
- At any rate, this is the method regularly used.

### Entropy of english
- As noted above, English in general is not a stationary ergodic process. 
- But we can nevertheless model it with various stochastic approximations. 
- In particular, we can model English with what are known as **n-gram models** or Markov chains. These models, where we assume a limited memory, we assume that the probability of the next word depends only on the previous k words in the input. This gives a kth order **Murkov approximation**:
$$\begin{aligned}P(X_n=x_n|X_{n-1}=x_{n=1},\dots,X_1=x_1)= \\
    P(X_n=x_n|X_{n-1} = x_{n-1},\dots,X_{n-k}=x_{n-k}) \end{aligned}$$
- If we are working on a character basis, for example, we are trying to guess what the next character in a text will be given the preceding k characters. Because of the redundancy of English, this is normally fairly easy. 
- For instance, a generation of students have proved this by being able to make do with photocopies of articles that are missing the last character or two of every line.
- By adding up counts of letters, letter digraphs (that is, sequences of two letters), and so on in English, one can produce upper bounds for the entropy of English. 
- We assume some such simplified model of English and compute its cross entropy against a text and this gives us an upper bound for the true entropy of English - since $D(p||m)\ge 0, H(X,m) \ge H(X)$.
- Shannon did this, assuming that English consisted of just 27 symbols (the 26 letters of the alphabet and SPACE - he ignored case distinctions and punctuation). The estimates he derived were:
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l">Model</th>
    <th class="tg-yw4l">Cross entropy (bits)</th>
    <th class="tg-yw4l">Remarks</th>
  </tr>
  <tr>
    <td class="tg-yw4l">Zeroth order</td>
    <td class="tg-yw4l">4.76</td>
    <td class="tg-yw4l">uniform model, log 27</td>
  </tr>
  <tr>
    <td class="tg-yw4l">First order</td>
    <td class="tg-yw4l">4.03</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">second order</td>
    <td class="tg-yw4l">2.8</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Shannon's experiment</td>
    <td class="tg-yw4l">1.3 (1.34)</td>
    <td class="tg-yw4l"></td>
  </tr>
</table>

- The first three lines show that as the order of the model increases, that is, as information about the frequencies of letters (first order) and digraphs (second order) is used, our model of English improves and the calculated cross entropy drops. 
- Shannon wanted a tighter upper bound on the entropy of English, and derived one by human experiments - finding out how good at guessing the next letter in a text a human being was. 
- This gave a much lower entropy bound for English. (A later experiment with more subjects on the same text that Shannon used produced the figure in parentheses, 1.34.)
- Of course, the real entropy of English must be lower still: there are doubtless patterns in people’s speech that humans do not pick up on (although maybe not that many!). 
- But at present, the statistical language models that we can construct are much worse than human beings, and so the current goal is to produce models that are as good as English speakers at knowing which English utterances sound normal or common and which sound abnormal or marked.

### Perplexity
- In the speech recognition community, people tend to refer to **perplexity** rather than cross entropy. The relationship between the two is simple
$$perplexity(x_{1n},m)=2^{H(x_{1n},m)}=m(x_{1n})^{-\frac{1}{n}} - - - -\dots(26)$$
- We suspect that speech recognition people prefer to report the larger non-logarithmic numbers given by perplexity mainly because it is much easier to impress funding bodies by saying that “we’ve managed to reduce perplexity from 950 to only 540” than by saying that “we’ve reduced cross entropy from 9.9 to 9.1 bits.” 
- However, perplexity does also have an intuitive reading: a perplexity of k means that you are as surprised on average as you would have been if you had had to guess between k equiprobable choices at each step.


```R

```
