---
title: Serverless
author: Bohdan (Dän) Chornokondratenko
theme:
    path: "goldbeck-theme.yaml"
    override:
        footer:
          style: template
          left: "{author}"
          right: "{current_slide} / {total_slides}"
---

kurz über mich
---

- September 2024: Praktikum bei GOLDBECK
- seit Oktober 2024 dualer Student in Informatik an der <span style="color:blue">DHSN</span> in Leipzig
<!-- speaker_note: Oktoberfest -->
<!-- pause -->
- Aussprache: <span style="color: red">~['bo:dan']~</span> <span style="color:green">[ˈdɛn]</span> / <span style="color:green">[bɔgˈdaːn]</span>
<!-- speaker_note: Slawischer Vornahme, Deutsch nicht meine Muttersprache -->
<!-- pause -->
- Vorerfahrung: <span>React</span>, Angular, (NodeJS) => Ziel: Fullstack
<!-- pause -->
- Speedcubing, Gitarre, Volleyball
<!-- pause -->
- I use neovim, btw

<!-- end_slide -->

Inhaltsverzeichnis
---
<!-- end_slide -->

Serverless? Hä? Was das?
---

<!-- column_layout: [1,1,1] -->

<!-- column: 0 -->
noch nie gehört:
![](./assets/face-with-open-mouth.png)
<!-- column: 1 -->
mal am Rande gehört:
![](./assets/clapping-hands.png)
<!-- column: 2 -->
kenne mich gut mit aus:
![](./assets/thumbs-up.png)

<!-- end_slide -->

Serverless = Einweg-Server
---

<!-- speaker_note: kein durchgehend laufender Server -->
<!-- speaker_note: alles andere leitet sich davon ab -->
<!-- speaker_note: darauf werde ich noch zurückkommen -->


<!-- pause -->
Warum soll mich das interessieren?
<!-- pause -->
- Pay as you go
<!-- pause -->
- Scale to zero
<!-- pause -->
- Automatic scaling
<!-- pause -->
- Geringerer Infra-Aufwand

<!-- end_slide -->

Werdegang
---

# bare metal/VM

- ein einzelner Server
- selbst Linux verwalten
- nur vertical Scaling

![](./assets/single-server.png) 

<!-- end_slide -->

Werdegang
---

# Cluster (horizontal scaling)

- Orchestrator (Load balancer)
- Alle Instanzen leben / on demand hochspinnen
- on demand: dauert => evtl. dead requests
- Overprovision vs Wartezeit

![](./assets/cluster.png) 
<!-- end_slide -->
Werdegang
---

# Cluster (horizontal scaling)

<!-- speaker_note: green - feste Anzahl an Instanzen passt perfekt, immer gleich belastet -->

![](./assets/usage-graph-1.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
![](./assets/usage-graph-2.png)
<!-- speaker_note: gelb - weniger optimal. idle time, overprovisioning -->
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
![](./assets/usage-graph-3.png)
<!-- speaker_note: threshhold - raten; Verzögerung  -->
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
![](./assets/usage-graph-4.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
![](./assets/usage-graph-5.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
![](./assets/usage-graph-5.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
## Singular instance startup
![](./assets/single-instance-1.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
## Singular instance startup
![](./assets/single-instance-2.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
![](./assets/single-instance-3.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)

<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/own-cluster.png)
<!-- column: 1 -->
<!-- pause -->
- ? wann sollen neue Instanzen hochgespinned werden
<!-- pause -->
- ? wie lange soll die neue Instanz leben
<!-- pause -->
- cold starts (node_modules, DB connection...)
<!-- pause -->
- muss stateless sein
<!-- pause -->
- "langsame" Reaktionszeiten

<!-- end_slide -->

Werdegang
---
# We accidentally invented *Serverless*!
<!-- speaker_note: bereits existierende Linux Umgebungen -->
![](./assets/serverless-1.png) 
<!-- end_slide -->

Werdegang
---
# We accidentally invented *Serverless*!
<!-- speaker_note: Node Runtime + Code wird nach Bedarf (Anfrage kommt) reingeladen -->
![](./assets/serverless-2.png) 
<!-- end_slide -->

Werdegang
---
# We accidentally invented *Serverless*!
![](./assets/serverless-3.png) 
<!-- end_slide -->

Werdegang
---
# We accidentally invented *Serverless*!
<!-- speaker_note: Anfrage => Instanz hochspinnen -> Bearbeitung -> Instanz töten, es sei denn gleich kommt noch was -->
<!-- speaker_note: deswegen Einweg-server -->
<!-- speaker_note: 10k Anfragen auf einmal => kein Ding! (Gefahr!) (Startups) -->
<!-- speaker_note: nur budget exceeded alerts bei AWS, keine Kostendeckelung -->

<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/serverless-4.png) 

<!-- column: 1 -->
- Lebenszyklus: Anfrage => Instanz hochspinnen => Bearbeitung => *Instanz töten
<!-- pause -->
*es sei denn gleich kommt noch was 

<!-- pause -->
- Automatic scaling
<!-- pause -->
- => Vorsicht! keine explizite Kostendeckelung bei AWS
<!-- pause -->
- Scale to zero
<!-- pause -->
- Geringerer Infra-Aufwand
<!-- pause -->
- Pay as you go
<!-- end_slide -->

Classisches Serverless
---
# Pay as you go
- GB*s (1 Sekunde Laufzeit von 1 Lambda Funktion mit 1 GB RAM)
<!-- pause -->

<!-- column_layout: [1,1,1] -->

<!-- column: 0 -->
![](./assets/serverless-pricing-1.png) 
<!-- pause -->

<!-- column: 1 -->
![](./assets/serverless-pricing-2.png) 
<!-- pause -->

<!-- column: 2 -->
![](./assets/serverless-pricing-3.png) 

<!-- reset_layout -->

# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
<!-- end_slide -->

# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
![](./assets/worker-1.png) 
<!-- end_slide -->

# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
![](./assets/worker-2.png) 
<!-- end_slide -->

# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?

<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/worker-3.png) 

<!-- pause -->
<!-- column: 1 -->
- "pay as you use"
<!-- pause -->
- Pricing: ms of CPU time
<!-- end_slide -->

Anwendbarkeit bei GOLDBECK
---
![image:width:60%](./assets/go2fries-lambda.png) 

<!-- end_slide -->

Offene Nachbarthemen
---
<!-- pause -->
- Edge (CDN, Edge Location, Edge Runtime)
<!-- pause -->
- SSR, PPR
<!-- pause -->
- DB sharding / DB replicating
<!-- pause -->
<!-- end_slide -->

Kapitel:
- Serverless im Allgemeinen
- Werdegang (VPS => k8s/ECS/AKS => Lambda => CF)
    * visuelles Schema VPS vs Cluster
    * Users/Time Graph
    * Serverful => Serverless Schema (mit Node etc)
    * nochmal Users/Time Graph
- Vor/Nachteile
- V8 (Cloudflare Workers)
- Anwendbarkeit bei GOLDBECK
- offene Nachbarthemen:
    * Edge (CDN, Edge Location, Edge Runtime)
    * SSR, PPR
    * DB sharding / DB replicating
- Acknowledgment (Theo)
- Bonus: Benchmarking tool for G2P
<!-- end_slide -->
---
 

```
theme:
  # Specify it by name for built-in themes
  name: my-favorite-theme

  # Otherwise specify the path for it
  path: /home/myself/themes/epic.yaml

  # Or override parts of the theme right here
  override:
    default:
      colors:
        foreground: white
---
```

<!-- end_slide -->
```


Headers
---

Using commonmark setext headers allows you to set titles for your slides (like seen above!):

<!-- speaker_note: this is also a speaker note -->
```
Headers
---
```

# Other headers

All other header types are simply treated as headers within your slide.

## Subheaders
### And more

<!-- end_slide -->

Slide commands
---

Certain commands in the form of HTML comments can be used:

# Ending slides

In order to end a single slide, use:

```html
<!-- end_slide -->
```

# Creating pauses

Slides can be paused by using the `pause` command:

```html
<!-- pause -->
```

This allows you to:

<!-- pause -->
* Create suspense.
<!-- pause -->
* Have more interactive presentations.
<!-- pause -->
* Possibly more!

<!-- end_slide -->

Code highlighting
---

Code highlighting is enabled for code blocks that include the most commonly used programming languages:

```rust
// Rust
fn greet() => &'static str {
    "hi mom"
}
```

```python
# Python
def greet() => str:
    return "hi mom"
```

```cpp
// C++
string greet() {
    return "hi mom";
}
```

And many more!

<!-- end_slide -->

Dynamic code highlighting
---

Select specific subsets of lines to be highlighted dynamically as you move to the next slide. Optionally enable line
numbers to make it easier to specify which lines you're referring to!

```rust {1-4|6-10|all} +line_numbers
#[derive(Clone, Debug)]
struct Person {
    name: String,
}

impl Person {
    fn say_hello(&self) {
        println!("hello, I'm {}", self.name)
    }
}
```

<!-- end_slide -->

Snippet execution
---

Code snippets can be executed:

* For various languages, including compiled ones.
* Their output is shown in real time.
* Unimportant lines can be hidden so they don't clutter what you're trying to convey.
* By default by pressing `<ctrl-e>`.

```rust +exec
# use std::thread::sleep;
# use std::time::Duration;
fn main() {
    let names = ["Alice", "Bob", "Eve", "Mallory", "Trent"];
    for name in names {
        println!("Hi {name}!");
        sleep(Duration::from_millis(500));
    }
}
```

<!-- end_slide -->

Images
---

Image rendering is supported as long as you're using iterm2, your terminal supports
the kitty graphics protocol (such as the kitty terminal itself!), or the sixel format.

* Include images in your slides by using `![](path-to-image.extension)`.
* Images will be rendered in **their original size**.
    * If they're too big they will be scaled down to fit the screen.

![](doge.png)

_Picture by Alexis Bailey / CC BY-NC 4.0_

<!-- end_slide -->

Column layouts
---

<!-- column_layout: [2, 1] -->

<!-- column: 0 -->

Column layouts let you organize content into columns.

Here you can place code:

```rust
fn potato() -> u32 {
    42
}
```

Plus pretty much anything else:
* Bullet points.
* Images.
* _more_!

<!-- column: 1 -->

![](doge.png)

_Picture by Alexis Bailey / CC BY-NC 4.0_

<!-- reset_layout -->

Because we just reset the layout, this text is now below both of the columns. Code and any other element will now look
like it usually does:

```python
print("Hello world!")
```

<!-- end_slide -->

Text formatting
---

Text formatting works as expected:

* **This is bold text**.
* _This is italics_.
* **This is bold _and this is bold and italic_**.
* ~This is strikethrough text.~
* Inline code `is also supported`.
* Links look like this [](https://example.com/)
* Text can be <span style="color: red">colored</span>.
* Text background color can be <span style="color: blue; background-color: black">changed too</span>.

<!-- end_slide -->

Other elements
---

Other elements supported are:

# Alerts

> [!caution]
> Github style alerts

# Tables

| Name | Taste |
| ------ | ------ |
| Potato | Great |
| Carrot | Yuck |

# Block quotes

> Lorem ipsum dolor sit amet. Eos laudantium animi ut ipsam beataeet
> et exercitationem deleniti et quia maiores a cumque enim et
> aspernatur nesciunt sed adipisci quis.

# Thematic breaks

A horizontal line by using `---`.

---
