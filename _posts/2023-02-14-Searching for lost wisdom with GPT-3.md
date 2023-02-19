---
title: "Searching for lost wisdom with GPT-3 📖🕵️"
excerpt: "Using GPT-3 to translate ancient texts"
permalink: /blog/searching-for-lost-wisdom-with-gpt-3/
date: 2023-02-14T15:34:30-04:00
categories:
  - blog
tags:
  - AI
  - NLP
  - coding
  - stoicism
  - philosophy
  - wisdom
---

TL;DR: I used GPT-3 to translate ancient texts, and found some interesting results. 
Skip to the [end](#final-thoughts) for a link to the final result.
## Introduction

Back in 2017, I had an almost religious experience. I was walking to work with my noise-cancelling headphones on under the hood of my jacket. It was late in the winter, but early in the morning. The wet snow whipped my face, eventually making my cheeks and forehead numb from the cold. But the cold didn't affect me. I had started to build "an Inner Citadel", being grateful for the cold, and for the snow, and for everything that is. I realized that we have the power to choose how we feel about things, and that we can choose to be grateful for everything that is - Turning obstacles upside down, and regard every difficulty as an opportunity to grow. To cultivate character. To become a better person.

The audiobook I was listening to was *Meditations* by Marcus Aurelius. 
I had recently been introduced to stoicism, through the book *Daily Stoic* by Ryan Holiday and Stephen Hanselman. This philosophy felt like it articulated my thoughts and feelings better than any other philosophy I had ever read. It felt like I had discovered an operating system for my mind, and eagerly absorbed each word.

I was on my way to work, but I was also on my way to a new life. I was on my way to a life of stoicism.

Since then, I have regularly revisited "Meditations", and bought several different versions (translations). Every time I skim through the book, I discover new gems of wisdom. 


## Lost in translation?

The original manuscript of *Meditations* was written in Ancient Greek (Even though Marcus Aurelius was Roman). Since then, there have been many translations, and many different versions of the book.
Several different manuscripts existed. One is in the Vatican library (Called Codex Vaticanus Graecus), but is apparently quite corrupted, and barely readable.
The other one, called codex Palatinus, was located in Basel, Switzerland, and was used as the source for the first printed edition of *Meditations* in 1588, by Wilhelm Xylander.
Several other manuscripts are olse known, but contain only fragments of the original text.

![Codices](/assets/images/codices.png)

Some of the other earliest translations are listed [here](https://en.wikisource.org/wiki/Meditations).

Some of the more recent, and more popular translations are listed below:
- [Meditations: A New Translation by Gregory Hays](https://www.amazon.com/Meditations-New-Translation-Marcus-Aurelius/dp/0812968255)
- [Meditations: with selected correspondence - Translation by Robin Hard](https://www.amazon.com/Meditations-selected-correspondence-Oxford-Classics-ebook/dp/B006QV7YN8/ref=sr_1_10?keywords=meditations+marcus+aurelius+robin+hard&qid=1676786309&s=books&sprefix=robin+hard%2Cstripbooks-intl-ship%2C164&sr=1-10)
- [The Emperor's Handbook: A New Translation of the Meditations of Marcus Aurelius](https://www.amazon.com/Emperors-Handbook-New-Translation-Meditations/dp/0743233832/ref=sr_1_7?keywords=meditations+marcus+aurelius+robin+hard&qid=1676786309&s=books&sprefix=robin+hard%2Cstripbooks-intl-ship%2C164&sr=1-7)

These translations are all great, but they are all different. They all have their own style, and some of them differ quite a bit in their interpretation of the original text.
Some translators have added their own commentary, and some have even added their own thoughts and ideas. We all have our own biases, and it is easy to see how these biases can creep into the translation process. It is also likely to assume that the later versions may have amplified biases from earlier translations.

I kept wondering how much the different translations had drifted from the original text. Was Marcus' original message conveyed accurately. Or had some of it been lost in translation?

With the recent advances in Natural Language Processing (NLP), I wondered if it was possible to use a Large Language Model (LLM) could do a good job in translating from Ancient Greek to English. 

A perfect "excuse" for me to get more familiar with the different GPT-models, the API, and how to best interact with them. 

## The Source

I wanted to find a text in ancient greek, hoping to find a version written in the same language as the original text would contain less bias. After some searching, I found a version of *Meditations* written in Ancient Greek, by the dutch poet and professor in classical languages, Jan Hendrik Leopold. This version was written in 1908, and was based on all the known manuscripts of *Meditations*.


## Translation is not a trivial task

Translation is not easy. This is something everyone who has tried to learn a new language knows. It is not just a matter of translating words. It is also a matter of translating the meaning of the words, and the context. This is especially true when translating texts from a completely different era, and from a completely different culture.

When using a LLM for this purpose, it will often help to feed the model with the necessary context, while also providing clear instructions on what we want the model to do.

As an example, let's take the following sentence from *Meditations*[^1] :

> "The Chaldeans and Astrologians having foretold the deaths of divers, were afterwards themselves surprised by the fates"

It is difficult to know whether the model has sufficient understanding of the Chaldeans to translate this sentence correctly. 
We could imagine that we could insert context about the entity "Chaldeans" from eg. Wikipedia, but this would still not guarantee a good understanding of the context.
Even if the model knows about the Chaldeans, it does not know what Marcus was referring to, with his particular perspective on the Chaldeans (in his time). 

[^1]: Translation by Meric Casaubon. 

## Preparing the text

### Beta code

The original text was written in Ancient Greek, and I discovered that using the [Beta Code](https://en.wikipedia.org/wiki/Beta_Code) system provided far better results than using the Greek alphabet. 
The Beta Code system is a system for writing Greek words using the Latin alphabet, which also captures the pronunciation of the Greek words, allowing for disambiguation of words with similar spelling.
### Keeping the sections

I needed to do some simple processing to keep the sections of the text intact as the chunks were of very different lengths.

For this, I need to give a small shoutout to Github Copilot.
Using Github Copilot has transformed the way I write code. It is a great tool, and I use it all the time. 
It offers a significant improvement to my workflow over using Stack Overflow, and is especially useful for writing snippets like the ones below.

```python
# Snippet to convert integer to roman numerals
def int_to_roman(input_number: int):
    """Convert an integer to a Roman numeral."""
    if not isinstance(input_number, type(1)):
        raise TypeError("expected integer, got %s" % type(input_number))
    if not 0 < input_number < 4000:
        raise ValueError("Argument must be between 1 and 3999")
    ints = (1000, 900,  500, 400, 100,  90, 50,  40, 10,  9,   5,  4,   1)
    nums = ('M',  'CM', 'D', 'CD','C', 'XC','L','XL','X','IX','V','IV','I')
    result = []
    for i in range(len(ints)):
        count = int(input_number / ints[i])
        result.append(nums[i] * count)
        input_number -= ints[i] * count
    return ''.join(result)
```

```python
def starts_with_romannumeral(text):
    # Regex to match a string that starts with a roman numeral, eg. I., II., IV., etc.
    # or starts with "BOOK IV" or "BOOK V" etc 
    text = text.strip()
    match = re.match(r"^[IVXLCDM]+\.", text) or re.match(r"^BOOK [IVXLCDM]+$", text)
    if match:
        return match[0]
    else:
        return ""
```

Seems like I am in good company

![karpathy](/assets/images/karpathy_twitter.png)

### Splitting

Another thing that is hard to do, is to provide the model with context from previous parts of the text. The maximum length of a result (prompt + generated) is 4096 tokens, so it is not possible to provide the model with the entire text produced thus far. So we need to strike a balance between providing enough context, while also keeping the chunks of text small enough to fit into the prompt, while still allowing the model to generate a reasonable amount of text.

I ended up splitting the text into chunks between 800 and 1300 tokens. 

## Providing context

A key part that underlies many of the opportunities to creating new applications with LLM's, is the ability to provide context to the model. This is done by providing the model with a prompt, which is the text that the model will use to generate the next text.

The prompt may be engineered in many different ways. You can retrieve factual information about entities, you can look up the most relevant paragraphs from your own Database, you can call external APIs, such as Wolfram Alpha, or even a Python REPL. 

**The opportunities are endless!**

For the purpose of this project, I settled on a simple approach. I wanted to provide translation examples dynamically. 

After some experimentation, I ended up using the following code to generate the prompts for the different translations:

```python
def translate_chunk(chunk, engine='text-davinci-003',
                    dest_language='English',
                    sample_translation=("BETA CODE: {sample_origin}, TRANSLATION: {sample_label}")
                    ):
    prompt = f'''Translate the text from ancient greek (beta code) to contemporary {dest_language}.
    Simplify the text, while keeping the meaning. The text is a part of the book "Meditations" by Marcus Aurelius.
    
    """
    {sample_translation[0]}
    {chunk}"""

    '''
    response = openai.Completion.create(
        prompt=prompt,
        engine=engine,
        temperature=0.1, 
        top_p=1,
        max_tokens= min([len(prompt)*2.2, 4096-len(prompt)]), # max 4096 tokens in total
    )
    result = response['choices'][0]['text'].strip()
    result = result.replace('"""', '') # remove the double quotes
    return result
```

There are quite a few things going on here, so let's break it down.

### Prompt

The prompt is the text that is fed to the model. It contains the instructions for the model, and the context that the model needs to understand the task at hand.
The first part is the instruction of the task. The second part is an example of the input and output that we want the model to produce. This is a very important part of the prompt, as it helps the model to understand what we want it to do, and has been shown to increase the quality of the results significantly.

To provide the model with sufficient context, we need to dynamically generate the prompt for each chunk of text to be translated. 

In my case, I found two strategies that increased the quality of the results significantly:
- Provide the model with a sample translation of the text. Choosing dynamically betweeen several sample translations enables me to choose the one that is most similar to chunk, and has a suitable length.

The translation examples i ended up using, was 10 handpicked translated sentences from Aristotle's "Ethics".
This may of course guide the model towards producing translations that are similar to Aristotle's, but through experimentation I found that the model did not emphasize the style of the translation too much, and that the results improved significantly by using this strategy.

- Giving the model context by saying that the text is a part of the book "Meditations" by Marcus Aurelius. As it is very likely that the book has been part of the model's training data, this should provide the model with more context. A potential downside of this is that the model may be biased towards earlier translations of the book. I ended up using this strategy, as I found that it produced better results.

### Engine

The engine is the model that we want to use. In this case, I used the `text-davinci-003` model. This is the most capable model for text generation. 
It produced the best results in my opinion, meaning that the output was most similar to other translations. `text-davinci-002` also produced seemingly good results, but I found that the translations were a bit too simplified, and lost some of the original meaning.

For other use cases, other models may be more suitable. For example when producing embeddings, the `text-embedding-ada-002` model is a better choice, and also significantly faster and cheaper to use.
To learn more about the different models, and how to use them, check out the [API documentation](https://platform.openai.com/docs/models/gpt-3).

### Parameters to tweak

The `temperature` parameter controls the randomness of the output. A higher temperature will result in more random output, while a lower temperature will result in more predictable output.
For translation, I found that a temperature of 0.1 produced the best results. We want the output to have just a little bit of randomness, to avoid repeating phrases and sentences, but we also want the output to be predictable, so that we can understand what the model is trying to say.

The `top_p` is an alternative to the `temperature` parameter to control the sampling of possible words to use for the output. 

## Results

Ok, enough talk. Let's see the results!

We'll use one of my favorite passages from *Meditations* as an example:

### Book III, Chapter 6 or 7 (depending on the translation)

[Ancient Greek translation by Jan Hendrik Leopold(1908)](https://www.perseus.tufts.edu/hopper/text?doc=Perseus%3Atext%3A2008.01.0641%3Abook%3D3%3Achapter%3D7%3Asection%3D1):

> Εἰ μὲν κρεῖττον εὑρίσκεις ἐν τῷ ἀνθρωπίνῳ βίῳ δικαιοσύνης, ἀληθείας, σωφροσύνης, ἀνδρείας καὶ καθάπαξ τοῦ ἀρκεῖσθαι ἑαυτῇ τὴν διάνοιάν σου, ἐν οἷς κατὰ τὸν λόγον τὸν ὀρθὸν πράσσοντά σε παρέχεται, καὶ ἐν τῇ εἱμαρμένῃ ἐν τοῖς ἀπροαιρέτως ἀπονεμομένοις: εἰ τούτου, φημί, κρεῖττόν τι ὁρᾷς, ἐπ᾽ ἐκεῖνο ἐξ ὅλης τῆς ψυχῆς τραπόμενος τοῦ ἀρίστου εὑρισκομένου ἀπόλαυε.

Google Translate:

> If, as a believer, you find in the human life justice, truth, sobriety, courage, and at the same time to satisfy yourself with your intellect, in which according to the word the right deed is provided for you, and in the admonition among those specially awarded: therefore, fame, Creton what do you see, on that with all his soul, running away from the excellent found, he enjoyed.

This seems like a direct word translation. Google translate is probably unable to understand that this text is Ancient Greek, not Contemporary greek, which results in a text that is not very coherent.

[English translation by Meric Casaubon(1634)](https://www.gutenberg.org/files/2680/2680-h/2680-h.htm#link2H_4_0035):

> "If thou shalt find anything in this mortal life better than righteousness, than truth, temperance, fortitude, and in general better than a mind contented both with those things which according to right and reason she doth, and in those, which without her will and knowledge happen unto thee by the providence; if I say, thou canst find out anything better than this, apply thyself unto it with thy whole heart, and that which is best wheresoever thou dost find it, enjoy freely.<br><br>But if nothing thou shalt find worthy to be preferred to that spirit which is within thee; if nothing better than to subject unto thee thine own lusts and desires, and not to give way to any fancies or imaginations before thou hast duly considered of them, nothing better than to withdraw thyself (to use Socrates his words) from all sensuality, and submit thyself unto the gods, and to have care of all men in general: if thou shalt find that all other things in comparison of this, are but vile, and of little moment; then give not way to any other thing, which being once though but affected and inclined unto, it will no more be in thy power without all distraction as thou oughtest to prefer and to pursue after that good, which is thine own and thy proper good. For it is not lawful, that anything that is of another and inferior kind and nature, be it what it will, as either popular applause, or honour, or riches, or pleasures; should be suffered to confront and contest as it were, with that which is rational, and operatively good.<br><br>For all these things, if once though but for a while, they begin to please, they presently prevail, and pervert a man's mind, or turn a man from the right way. Do thou therefore I say absolutely and freely make choice of that which is best, and stick unto it. Now, that they say is best, which is most profitable. If they mean profitable to man as he is a rational man, stand thou to it, and maintain it; but if they mean profitable, as he is a creature, only reject it; and from this thy tenet and conclusion keep off carefully all plausible shows and colours of external appearance, that thou mayest be able to discern things rightly."

Causabon obviously capture a lot more of the meaning of the text, but it is still a bit hard to read, which is not so strange, considering that the text was written almost 500 years ago.

[English translation by George Long (1862)](http://classics.mit.edu/Antoninus/meditations.3.three.html):

> If thou findest in human life anything better than justice, truth, temperance, fortitude, and, in a word, anything better than thy own mind's self-satisfaction in the things which it enables thee to do according to right reason, and in the condition that is assigned to thee without thy own choice; if, I say, thou seest anything better than this, turn to it with all thy soul, and enjoy that which thou hast found to be the best.<br><br>But if nothing appears to be better than the deity which is planted in thee, which has subjected to itself all thy appetites, and carefully examines all the impressions, and, as Socrates said, has detached itself from the persuasions of sense, and has submitted itself to the gods, and cares for mankind; if thou findest everything else smaller and of less value than this, give place to nothing else, for if thou dost once diverge and incline to it, thou wilt no longer without distraction be able to give the preference to that good thing which is thy proper possession and thy own; for it is not right that anything of any other kind, such as praise from the many, or power, or enjoyment of pleasure, should come into competition with that which is rationally and politically or practically good.<br><br>All these things, even though they may seem to adapt themselves to the better things in a small degree, obtain the superiority all at once, and carry us away. But do thou, I say, simply and freely choose the better, and hold to it.- But that which is useful is the better.- Well then, if it is useful to thee as a rational being, keep to it; but if it is only useful to thee as an animal, say so, and maintain thy judgement without arrogance: only take care that thou makest the inquiry by a sure method.

This is even more readable, but still requires a lot of effort to understand, for those of us who are not used to reading classical English.

[Translation by Gregory Hays(2003)](https://ia600906.us.archive.org/12/items/meditation-GeorgeHays/meditations-GeorgeHays.pdf):
>If, at some point in your life, you should come across anything better than justice, honesty, self-control, courage— than a mind satisfied that it has succeeded in enabling you to act rationally, and satisfied to accept what’s beyond its control—if you find anything better than that, embrace it without reservations—it must be an extraordinary thing indeed—and enjoy it to the full.<br><br>But if nothing presents itself that’s superior to the spirit that lives within—the one that has subordinated individual desires to itself, that discriminates among impressions, that has broken free of physical temptations (as Socrates used to say), and subordinated itself to the gods, and looks out for human beings’ welfare—if you find that there’s nothing more important or valuable than that - then don’t make room for anything but it—for anything that might lead you astray, tempt you off the road, and leave you unable to devote yourself completely to achieving the goodness that is uniquely yours. It would be wrong for anything to stand between you and attaining goodness—as a rational being and a citizen. Anything at all: the applause of the crowd, high office, wealth, or self-indulgence. All of them might seem to be compatible with it—for a while. But suddenly they control us and sweep us away. So make your choice straightforwardly, once and for all, and stick to it.<br><br>Choose what’s best. —Best is what benefits me. As a rational being? Then follow through. Or just as an animal? Then say so and stand your ground without making a show of it. (Just make sure you’ve done your homework first.)

This translation has over 1400 ratings on Amazon, ranks as #1 in "Greek and Roman philosophy", topped the bestseller lists in 2003, and is considered of many (including Ryan Holiday) to be the best translation of the Meditations. 
Some critics have pointed out that Hays have taken a bit too much liberty with the text, and that too much of his own opinion is present in the translation. I don't know if this is true, but I do know that the translation is very enjoyable to read.

`text-davinci-002`:	
> If you find a ruler in human affairs who is just, truthful, temperate, brave and able to bring his own thoughts into accord with the right, as expressed in words, and in the harmony of things done without compulsion; if you find such a one, say, in a single place, turning away from the multitude of the unjust, then you have found a rare thing. But if you find no such ruler, then let him, as Socrates said, look to himself and examine his own thoughts and feelings, and let him subject himself to the gods and to the laws of men; and if he can do all this, then let him consider all the rest as secondary and of less importance.<br><br>For it is not easy to oppose the just and the political good, nor is it possible to bring together things so diverse as the opinion of the many and the rule of law, or the power of a tyrant, or wealth, or the pleasures of the senses; all these, however, he has set aside and rejected. But you, I say, should simply and freely take the ruler and accept him; and let the ruler be the one who is friendly. If it is as a just man, then keep him; but if as a living man, then let him go, and with safety make your choice.<br><br>Never forget to be mindful of yourself, to be willing to accept whatever fate may bring, to be ready to help those in need, to show compassion, to forgive, to be humble, and to build walls and barriers for the protection of others. For your own mind and spirit, and the actions of this virtue, must be guarded.

`text-davinci-003`(`temperature=0`):

> If you find something better in human life than justice, truth, self-control, courage and moderation, use your reason to hold on to it and in the face of all external temptations remain devoted to it. If nothing better appears, then accept the divine element within you and examine your own impressions and feelings, as Socrates said, without conceit and with due respect for the gods and for other people. If you find all other things to be small and secondary, give no place to anything else, but keep your attention firmly on that which is good in itself, your own and unique.<br><br>For it is not difficult to be devoted to the rational and political good, such as fame, power, wealth, or pleasure. All these things, however, have been taken away and left behind. You, however, should simply and freely take hold of the better and cling to it. If it is the rational good, then keep it. If it is the natural good, then accept it and make a safe decision.<br><br>Honor yourself by accepting what you must do, even when it is difficult to bear, such as enduring pain, giving up something you want, being kind to someone you dislike, controlling your anger, forgiving someone, and wanting what is good for someone else. For your mind and spirit, and the actions that come from them, should be free from all restraint.<br><br>Do not do anything extravagant, do not be ostentatious, do not be angry, do not try to outdo others. The greatest thing is to live without either pursuing or fleeing from anything, and to use the time given to us by our body and soul in the best way possible. We should accept our fate and move on, as if we were just another part of the universe, and use our life to nourish our intelligence and make it grow.

`text-davinci-003` (`temperature=0.1`):

> If you find something better in human life than justice, truth, self-control, courage and moderation, use your reason to hold on to it and in the face of all distractions, keep it in mind. If nothing better appears, then accept the divinely appointed order of things and be content with it, examining your own dispositions and controlling your impulses, as Socrates said, humbly and reverently submitting to the gods and to your fellow human beings. If you do this, you will have no need of anything else, and you will be able to keep your attention on the good, your own and that of others, without distraction.<br><br>For it is not necessary to seek out many different things, such as fame among the many, or power, or wealth, or sensual pleasures; all these things, if they come in small amounts, are enough to make life pleasant. So simply and easily accept the better and cling to it. If it is according to reason, keep it; if according to custom, let it go, but with a good conscience. Only make sure that your choice is safe.<br><br>Never be ashamed of doing what is necessary, such as submitting to authority, enduring hardship, making sacrifices, being humble, apologizing, or asking for help. For it is your own mind and spirit, and the actions of this self-control, that you should be proud of.<br><br>We should not do anything extravagant, nor be anxious, nor angry; nor should we try to acquire more than is necessary: the greatest thing is to live in harmony, neither fawning nor avoiding people, and to use the present time with moderation, either in the body or in the soul, without being attached to anything. For it is already time to let go and to pass away, as if it were something natural and common in the world, and to use life only to make the mind better, and to be nourished by a wise and political animal.

Here is the final translation:

![Cover](/assets/images/Cover.jpg)

[Pdf](/assets/pdfs/Meditations%20-%20Marcus%20Aurelius%20(Translation%20from%20ancient%20greek%20with%20AI).pdf)


## Final thoughts 

I think the results are quite good, especially considering this was a side project done in a few hours.
I actually considered putting even more effort into this translation, and sell it on Amazon.
But I decided against it. For me, the main purpose of this project was to dive deeper into LLM's for my work as a Data Scientist.

Therefore, I decided to keep the produced texts completely unchanged, even though I saw some obvious room for improvement.
If I had intended to make money off the translation, a bit more manual intervention would have been necessary.

For writers and translators, I would recommend to learn more about LLM's and try to use them as aids in their work. 

#### More languages, adapted to the target audience

Translation to different languages would be as simple as changing the `dest_language` -parameter. (And perhaps finding a few good examples).
I tested this with Norwegian, and the results were quite good. Hopefully, minority languages would also benefit from this approach.
By modifying the prompt slightly, it would also be possible to generate poetry, text suitable for children, or another target audience.

#### Other sources

There are a lot of classical texts out there, and I would love to see more modern translations of them.

#### Multimodality

The only thing stopping me from creating an audiobook version is that current Speech-to-Text software cost a bit more than I was willing to pay.
Give it a year, and I feel confident that I could create a high-quality audiobook version with open-source tools.

Another cool idea would be to generate graphic novels, using tools such as Stable Diffusion, Midjourney or DALL-E.

#### Information overflow?

Even though I am a notorious technology optimist, I think it is necessary to add a small concern. It is easy to imagine a future where AI generates so much content that it becomes impossible to keep up with it, and that we lose the ability to distinguish between original content and AI-generated content.

I think that the best way to think about these exciting new tools are as tools, that can augment and complement our own abilities, rather than as replacements.
Our strengths and weaknesses are complementary, and we should use them to our advantage.

### Acknowledgements

Thanks to te Perseus Project for providing the original (beta code)-version of the text.
