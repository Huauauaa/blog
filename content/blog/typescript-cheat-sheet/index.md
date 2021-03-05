---
title: typescript-cheat-sheet
date: '2021-03-05'
description: 'typescript'
---

> Something about typescript.

## Property 'dataset' does not exist on type 'EventTarget'

![ts-1](./ts-1.png)

```ts
private onContextmenuItemClick(vm: unknown, event: PointerEvent) {
  const target = event.target as HTMLElement;
  console.log(this.currentKey, target.dataset.name);
}

```
