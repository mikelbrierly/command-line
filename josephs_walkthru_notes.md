# Rebel Traitor Hunt

Joseph's Notes

## Start

Check out the repo and read the first file.

```bash
git clone https://github.com/mikelbrierly/star-wars-command-line.git && \
  cd star-wars-command-line-master/rebel-traitor-hunt/ && \
  cat instructions-from-vader
```

Ok, find **traitor** and **SECURITY-BREACH**

`../contact_vader` is the answer file to confirm.

Protect that for now.

`chmod 000 contact_vader`

## Investigation

Examine the layout

`cd death-star; tree -d`

Don't want to accidentally cat the hints

`rm -f hint*`

Ok let's go.

`grep -i traitor interviews/*`

```text
interview-699607:Trooper stated that the only intel she has is that the traitors armor was severely battle damaged, a late Kamino make, and had a TK ID number that starts with a "113" and ends in an "8".
```

`less armor-info`

Too many, but shows the formatting of the data.

`less imperial-personnel`

Too many. But it gives the look up hint at the beginning.

```text
Alexsandr Kallus        M       36      Lothal Barracks, line 318
Line 318 of "barracks/Lothal"
```

### Armor

Find the armor

`grep -B1 -i 'kamino' armor-info | grep '113'`

These all end with `-8` already. Let's get the clean numbers

`grep -B1 -i 'kamino' armor-info | grep '113' | cut -d\# -f2 | tr -d ' '`

Build first suspect list with that info.

`for xx in $(grep -B1 -i 'kamino' armor-info | grep '113' | cut -d\# -f2 | tr -d ' '); do printf '\n'; grep -A5 $xx armor-info; done >> mysuspects.txt`

Distill the data into a list of names

`grep Owner mysuspects.txt | cut -d: -f2 | cut -d\  -f2-`

Find out about these people. Input field separator will need to be newline for spaces to work in the loop.

`IFS=$(echo -en "\n\b"); for xx in $(grep Owner mysuspects.txt | cut -d: -f2 | cut -d\  -f2-); do grep $xx imperial-personnel; done`

Hmm no results.

### Memberships

What are memberships?

`IFS=$(echo -en "\n\b"); for xx in $(grep Owner mysuspects.txt | cut -d: -f2 | cut -d\  -f2-); do grep $xx memberships/*; done`

What are these files?

### Security Breaches

I forgot about the breach! Let's try that one.

`grep SECURITY-BREACH stormtrooper-report-log`

Three new clues:

```text
SECURITY-BREACH: It appears that this may be an inside job. Footage from a mouse droid is blurry but shows that the traitor is a tall male, at least 6', wearing stormtrooper armor.
SECURITY-BREACH: The last known retinal scan of the traitor shows that he is affiliated with the Imperial Dejarik Club, Blue Milkaholics Anonymous, Ewotic Ewoks, and Aim Like A Stormtrooper 101. The rest of the data showing his name and identity have been tampered with...
SECURITY-BREACH: A female trooper with the alias of "Salacius" was the last known trooper to have interacted with the traitor.
```

### Suspect List Narrows

Someone imperial, male, tall, clubs, and check into reports. This narrows the suspects.

`grep -A1 -B4 "Height: 6" mysuspects.txt > mysuspects2.txt`

`IFS=$(echo -en "\n\b"); for xx in $(grep Owner mysuspects2.txt | cut -d: -f2 | cut -d\  -f2-); do grep $xx memberships/*; done`

```text
memberships/Aim_Like_A_Stormtrooper_101:Richard LeParmentier
memberships/Blue_Milkaholics_Anonymous:Richard LeParmentier
memberships/Ewotic_Ewoks:Richard LeParmentier
memberships/Imperial_Dejarik_Club:Richard LeParmentier
memberships/Aim_Like_A_Stormtrooper_101:Janthaus Staucks
```

> (Looking back, I could have stopped here, but I wasn't sure if I had all of the evidence yet!)

### Barracks

What's in the barracks?

`grep traitor barracks/*`

Gibberish

Check into this Salacius woman.

`grep Salacius armor-info`

Not a trooper.

`grep -n Salacius imperial-personnel`

Two females match out of four people with this name.

```text
298:Salacius Sun        F       26      Plasteel Barracks, line 40
1690:Salacius Church    F       38      Bespin Barracks, line 179
```

Let's check out this barracks.

`head -n 40 barracks/Plasteel | tail -1`

```text
SEE INTERVIEW #47246024
```

`grep "SEE INTERVIEW" barracks/*`

Too many.

>(That result list turned out to be a bug!)

Try the other barracks.

`head -n 179 barracks/Bespin | tail -1`

`SEE INTERVIEW #699607`

These refer to files. We've seen 66907 already from earlier.

`cat interviews/interview-47246024`

`This trooper has been on holiday in Utapau for the last 3 weeks, has no intel.`

## Getting Sidetracked

### Palpatine's Journal

HM. I'm a bit confused. Let's reread the original starting document and try keywords. Also what could be in Palpatine's journal?

`grep -Pi 'go+?d' palpatines-personal-journal`

Heh.

`grep -ri "Richard LeParmentier" *`

`grep -ri "Janthaus Staucks" *`

`grep -ri documents *`

`grep -ri force *`

`palpatines-personal-journal:MY_GRANDMA HAS BETTER FORCE LIGHTING THAN SHEEV PALPATINE - TRAITOR WUZ HERE`

LOL

`grep -ri SHEEV`

`palpatines-personal-journal:I CANT_BELIEVE THE EMPEROR'S NAME IS SHEEV! - TRAITOR WUZ HERE`

The signature seems consistent.

`grep -i traitor palpatines-personal-journal`

```text
THE EMPEROR IS BANTHA_POODOO - TRAITOR WUZ HERE
THE EMPEROR IS A PRUNE_FACED MYNOCK GOBBLER! - TRAITOR WUZ HERE
```

### Rechecking Members

`grep -ri membership *`

`interviews/interview-29741223:Should not be considered a suspect, has no SkyMiles membership and has never been a member of the Museum of Bash History.`

>(Bug remnants!)

`grep -ri 'has never' *`

```text
interviews/interview-174898:The license plate of Keefe's Mazda matches the witness's description, but the make is wrong, and Keefe has never been a SkyMiles member.  Shouldn't be considered a suspect.
interviews/interview-29741223:Should not be considered a suspect, has no SkyMiles membership and has never been a member of the Museum of Bash History.
interviews/interview-30259493:Shaw knew the victim, but has never been a SkyMiles member and has a solid alibi for the morning in question.  Not considered a suspect.
```

`grep -ri skymiles`

`interviews/interview-290346:Is a SkyMiles, TCPL, Museum of Bash History, and AAA member.`

`grep -ri "license" *`

```text
interviews/interview-56892213:He's tall enough to be a suspect, but he drives a Subaru, not a Honda, and the license plate doesn't match.
interviews/interview-737609:Keller's car matches the description, but not his license plate.
```

### Keller and Killer

`grep -ri keller`

`interviews/interview-737609:Keller is also shorter than the killer.`

Killer? We are looking for an infiltrator. What is this, a subplot? With cars?

`grep -ri killer`

```
interviews/interview-2939888:Billings should not be considered a suspect, she is too short to match the camera footage and the killer is believed to be male.
```

`grep -ri Billings`

```text
armor-info:Owner: Heather Billings
imperial-personnel:Heather Billings     F       38      Culbert Barracks, line 19
```

That line 19 just leads back to the interview found.

`grep -C6 "Heather Billings" armor-info`

```text
TK ID#  L337369
Make: Utapau
Condition: Pristine
Owner: Heather Billings
Height: 5'2"
Weight: 244 lbs
```

`grep -C6 "Al Shaw" imperial-personnel`

```text
TK ID#  L337X19
Make: Geonosis
Condition: Pristine
Owner: Al Shaw
Height: 6'5"
Weight: 240 lbs
```

I dont know if this goes anywhere.

### Did the Traitor Leave Clues?

Why would the traitor use underscores in the log?

`grep -ri prune_faced *`

`grep -ri bantha_poo *`

`grep -ri cant_believe *`

`grep -ri my_grandma *`

Well his paternal grandmother is not an imperial citizen or stormtrooper.

### Re-examine Interviews

Let's recheck all SEE INTERVIEWS then.

`for xx in $(grep "SEE INTERVIEW" barracks/* | cut -d\# -f2); do echo -ne $xx": "; cat interviews/interview-$xx | tr -s '\n' ' '; echo; done`

Hmm that's a lot data.

>(And wasn't supposed to be there!)

Reference barracks lines.

`grep -n "SEE INTERVIEW" barracks/* | cut -d/ -f2 | cut -d: -f1-2 | tr -s ':' ' '`

Cross-reference their interview to their personnel file.

`IFS=$(echo -en "\n\b"); for xx in $(grep -n "SEE INTERVIEW" barracks/* | cut -d/ -f2 | cut -d: -f1-2 | tr -s ':' ' '); do aa=$(echo $xx | cut -d\  -f1 | tr -d '_'); bb=$(echo $xx | cut -d\  -f2); grep $aa imperial-personnel | grep $bb; grep $(echo $xx | cut -d\  -f2) barracks/$(echo $xx | cut -d\  -f1); done`

This is also a lot more data.

## Conclusion

At this point I'm going to go with the guy connected to the most clubs, TK 113Q4H8 Richard LeParmentier

`echo "113Q4H8" | $(command -v md5 || command -v md5sum) | grep -qif .5dmtcerroc && echo "$(cat .5dmrewsna)" || echo "$(cat .5dmgnorw)"`

Vader is pleased.
