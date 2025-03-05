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
1. Serverless kurz gesagt
<!-- pause -->
2. Werdegang
<!-- pause -->
3. Classisches Serverless
<!-- pause -->
4. Cloudflare Workers
<!-- pause -->
5. Anwendbarkeit bei GOLDBECK
<!-- pause -->
6. (Bonus: Benchmarking-Codeschnipsel)

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
- Abwechslung von der Enterprise-Welt
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

- orchestrator (Load balancer)
- alle Instanzen leben / on demand hochspinnen
- on demand: dauert => evtl. dead requests
- overprovision vs Wartezeit

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
<!-- speaker_note: das alte Threshhold reicht nicht aus -->
![](./assets/usage-graph-4.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
<!-- speaker_note: overprovisioning (Leerlaufzeiten) -->
![](./assets/usage-graph-5.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
## Singular instance dynamic startup
![](./assets/single-instance-1.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
## Singular instance dynamic startup
![](./assets/single-instance-2.png)
<!-- end_slide -->

Werdegang
---
# Cluster (horizontal scaling)
## Singular instance dynamic startup
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
<!-- speaker_note: langsame Reaktionszeiten ist letzter Punkt, dann Serverless -->

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
![](./assets/serverless-4.png) 
<!-- end_slide -->

Werdegang
---
# We accidentally invented *Serverless*!

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

<!-- pause -->
# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
<!-- end_slide -->

Cloudflare Workers
---
# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
![](./assets/worker-1.png) 
<!-- end_slide -->

Cloudflare Workers
---
# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
![](./assets/worker-2.png) 
<!-- end_slide -->

Cloudflare Workers
---
# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?
![](./assets/worker-3.png) 
<!-- end_slide -->

Cloudflare Workers
---
# Luft nach oben: lange Ausführungszeit aber wenig CPU-Last?

<!-- column_layout: [1,1] -->
<!-- column: 0 -->
![](./assets/worker-3.png) 

<!-- pause -->

<!-- column: 1 -->
- V8: JS Engine (von Google), wird benutzt im Browser
<!-- speaker_note: Bun - WebKit's JavaScriptCore, Node/Deno - V8 -->
<!-- speaker_note: von Runtime trennen -->
<!-- speaker_note: Isolates - eigener Heap etc, komplette Isolierung -->

<!-- pause -->
- "pay as you use"
<!-- pause -->
- Pricing: ms of CPU time
<!-- end_slide -->

Anwendbarkeit bei GOLDBECK
---
<!-- pause -->
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
<!-- end_slide -->

Acknowledgment
---
![image:width:40%](./assets/theo-channel.png) 
![image:width:40%](./assets/theo-video.png) 

<!-- end_slide -->

Bonus: Benchmarking-Codeschnipsel
---

- Ausgangspunkt: eine Klasse mit echten Daten benchmarken (Go2Price, Parsing von 10k+ Formeln)
<!-- pause -->
- Probleme beim händischen Testing:
<!-- pause -->
  * umständlich im UI nachzustellen
<!-- pause -->
  * Input nicht immer identisch
<!-- pause -->
  * die gesamte Aufrufkette dauert viel länger als das, was wir benchmarken wollen
<!-- pause -->
  * 100 mal aufrufen und Durchschnitt nehmen - geht nicht
<!-- pause -->
- Lösung: Payload in IndexedDB persistieren
<!-- speaker_note: nach `Lösung` im Browser zeigen... -->

<!-- end_slide -->

Bonus: Benchmarking-Codeschnipsel
---

<!-- column_layout: [3,2] -->
<!-- column: 0 -->
```ts
constructor() {
  window.benchmark = async (method, qty = 1) => {
    if (!this[method]) {
      console.log('invalid method');
      return;
    }

    const payload = await readFromDB(method);
    if (!payload) {
      console.log('no cached payload');
      return;
    }

    const results = [];
    for (let i = 0; i < qty; i++) {
      const start = performance.now();
      await firstValueFrom(this[method](payload));
      const end = performance.now();
      results.push(end - start);
    }

    const sum = results.reduce((prev, cur) => prev + cur, 0)
    const avg = sum / results.length;
    console.log('Avg: ', avg);
  };
}
```
<!-- column: 1 -->

```ts
@PersistForBenchmarking
public updateFormulasOnFormulasRemovedAndAdded$({
```

```ts
function PersistForBenchmarking(
  _target: any,
  propertyKey: string,
  descriptor: TypedPropertyDescriptor<Function>
) {
  const originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) {
    writeToDB(propertyKey, args[0]);
    return originalMethod.apply(this, args);
  };
}
```

<!-- end_slide -->
Bonus: Benchmarking-Codeschnipsel
---

<!-- column_layout: [1,1,1] -->
<!-- column: 0 -->
```ts
/* eslint-disable @typescript-eslint/no-explicit-any */
const dbName = 'MyDatabase';
const storeName = 'MyStore';

// Open (or create) the database
const request = indexedDB.open(dbName, 1);

request.onupgradeneeded = (event: IDBVersionChangeEvent) => {
  const db = (event.target as IDBOpenDBRequest).result;

  if (!db.objectStoreNames.contains(storeName)) {
    db.createObjectStore(storeName, { keyPath: 'id' });
  }
};

request.onsuccess = () => {
  console.log('Database initialized successfully');
};
```

<!-- column: 1 -->
```ts
// Function to write a string to the database with a specific key
export function writeToDB(
  key: number | string,
  value: unknown,
  logOnComplete = false
): void {
  const request = indexedDB.open(dbName, 1);
  const serializedValue = JSON.stringify(value);

  request.onsuccess = (event: Event) => {
    const db = (event.target as IDBOpenDBRequest).result;
    const transaction = db.transaction(storeName, 'readwrite');
    const store = transaction.objectStore(storeName);

    store.put({ id: key, value: serializedValue });

    transaction.oncomplete = () => {
      if (logOnComplete)
        console.log(`Data written for key ${key}:`, serializedValue);
    };

    transaction.onerror = () => {
      console.error('Write transaction failed:', transaction.error);
    };
  };

  request.onerror = () => {
    console.error('Database error:', request.error);
  };
}
```

<!-- column: 2 -->
```ts
// Function to read a string from the database by key
export function readFromDB(key: number | string): Promise<any | null> {
  return new Promise((resolve, reject) => {
    const request = indexedDB.open(dbName, 1);

    request.onsuccess = (event: Event) => {
      const db = (event.target as IDBOpenDBRequest).result;
      const transaction = db.transaction(storeName, 'readonly');
      const store = transaction.objectStore(storeName);

      const getRequest = store.get(key);

      getRequest.onsuccess = () => {
        resolve(getRequest.result ? JSON.parse(getRequest.result.value) : null);
      };

      getRequest.onerror = () => {
        reject(new Error('Read transaction failed'));
      };
    };

    request.onerror = () => {
      reject(new Error('Database error'));
    };
  });
}
```


<!-- end_slide -->

Vielen Dank für eure Aufmerksamkeit!
---
![image:width:30%](./assets/pepe.png)

<!-- end_slide -->
