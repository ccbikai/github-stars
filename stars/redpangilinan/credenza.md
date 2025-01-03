---
project: credenza
stars: 629
description: Ready-made responsive modal component for shadcn/ui.
url: https://github.com/redpangilinan/credenza
---

Credenza
========

A responsive modal component for shadcn/ui.

Installation
------------

1.  Copy the `dialog` and `drawer` component from shadcn/ui.

npx shadcn@latest add dialog drawer

Alternatively, if you are not using shadcn/ui cli, you can manually copy the components from shadcn/ui or directly copy from dialog.tsx and drawer.tsx.

If you copied the drawer component manually, make sure to install vaul.

```
npm install vaul
```

1.  Copy the `useMediaQuery` hook: use-media-query.tsx

import \* as React from "react"

export function useMediaQuery(query: string) {
  const \[value, setValue\] \= React.useState(false)

  React.useEffect(() \=> {
    function onChange(event: MediaQueryListEvent) {
      setValue(event.matches)
    }

    const result \= matchMedia(query)
    result.addEventListener("change", onChange)
    setValue(result.matches)

    return () \=> result.removeEventListener("change", onChange)
  }, \[query\])

  return value
}

1.  Copy the `credenza` component: credenza.tsx

Click to show code

"use client"

import \* as React from "react"

import { cn } from "@/lib/utils"
import { useMediaQuery } from "@/hooks/use-media-query"
import {
  Dialog,
  DialogClose,
  DialogContent,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog"
import {
  Drawer,
  DrawerClose,
  DrawerContent,
  DrawerDescription,
  DrawerFooter,
  DrawerHeader,
  DrawerTitle,
  DrawerTrigger,
} from "@/components/ui/drawer"

interface BaseProps {
  children: React.ReactNode
}

interface RootCredenzaProps extends BaseProps {
  open?: boolean
  onOpenChange?: (open: boolean) \=> void
}

interface CredenzaProps extends BaseProps {
  className?: string
  asChild?: true
}

const desktop \= "(min-width: 768px)"

const Credenza \= ({ children, ...props }: RootCredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const Credenza \= isDesktop ? Dialog : Drawer

  return <Credenza {...props}\>{children}</Credenza\>
}

const CredenzaTrigger \= ({ className, children, ...props }: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaTrigger \= isDesktop ? DialogTrigger : DrawerTrigger

  return (
    <CredenzaTrigger className\={className} {...props}\>
      {children}
    </CredenzaTrigger\>
  )
}

const CredenzaClose \= ({ className, children, ...props }: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaClose \= isDesktop ? DialogClose : DrawerClose

  return (
    <CredenzaClose className\={className} {...props}\>
      {children}
    </CredenzaClose\>
  )
}

const CredenzaContent \= ({ className, children, ...props }: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaContent \= isDesktop ? DialogContent : DrawerContent

  return (
    <CredenzaContent className\={className} {...props}\>
      {children}
    </CredenzaContent\>
  )
}

const CredenzaDescription \= ({
  className,
  children,
  ...props
}: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaDescription \= isDesktop ? DialogDescription : DrawerDescription

  return (
    <CredenzaDescription className\={className} {...props}\>
      {children}
    </CredenzaDescription\>
  )
}

const CredenzaHeader \= ({ className, children, ...props }: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaHeader \= isDesktop ? DialogHeader : DrawerHeader

  return (
    <CredenzaHeader className\={className} {...props}\>
      {children}
    </CredenzaHeader\>
  )
}

const CredenzaTitle \= ({ className, children, ...props }: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaTitle \= isDesktop ? DialogTitle : DrawerTitle

  return (
    <CredenzaTitle className\={className} {...props}\>
      {children}
    </CredenzaTitle\>
  )
}

const CredenzaBody \= ({ className, children, ...props }: CredenzaProps) \=> {
  return (
    <div className\={cn("px-4 md:px-0", className)} {...props}\>
      {children}
    </div\>
  )
}

const CredenzaFooter \= ({ className, children, ...props }: CredenzaProps) \=> {
  const isDesktop \= useMediaQuery(desktop)
  const CredenzaFooter \= isDesktop ? DialogFooter : DrawerFooter

  return (
    <CredenzaFooter className\={className} {...props}\>
      {children}
    </CredenzaFooter\>
  )
}

export {
  Credenza,
  CredenzaTrigger,
  CredenzaClose,
  CredenzaContent,
  CredenzaDescription,
  CredenzaHeader,
  CredenzaTitle,
  CredenzaBody,
  CredenzaFooter,
}

1.  Update the import paths based on your project structure.
    
2.  If you want to enable background scaling, wrap your app with the `vaul-drawer-wrapper`.
    

<div vaul-drawer-wrapper\="" className\="bg-background"\>{children}</div\>

See my implementation at layout.tsx. Make sure to update the background color to match your project's theme.

Usage
-----

import {
  Credenza,
  CredenzaBody,
  CredenzaClose,
  CredenzaContent,
  CredenzaDescription,
  CredenzaFooter,
  CredenzaHeader,
  CredenzaTitle,
  CredenzaTrigger,
} from "@/components/ui/credenza"

Basic usage with `CredenzaTrigger`

<Credenza\>
  <CredenzaTrigger asChild\>
    <button\>Open modal</button\>
  </CredenzaTrigger\>
  <CredenzaContent\>
    <CredenzaHeader\>
      <CredenzaTitle\>Credenza</CredenzaTitle\>
      <CredenzaDescription\>
        A responsive modal component for shadcn/ui.
      </CredenzaDescription\>
    </CredenzaHeader\>
    <CredenzaBody\>
      This component is built using shadcn/ui&apos;s dialog and drawer
      component, which is built on top of Vaul.
    </CredenzaBody\>
    <CredenzaFooter\>
      <CredenzaClose asChild\>
        <button\>Close</button\>
      </CredenzaClose\>
    </CredenzaFooter\>
  </CredenzaContent\>
</Credenza\>

Using state to open modal

function StateModal() {
  const \[open, setOpen\] \= React.useState(false)

  const handleOpen \= () \=> {
    setOpen(true)
  }

  return (
    <\>
      <Button onClick\={handleOpen}\>Open with State</Button\>

      <Credenza open\={open} onOpenChange\={setOpen}\>
        <CredenzaContent\>
          <CredenzaHeader\>
            <CredenzaTitle\>Credenza</CredenzaTitle\>
            <CredenzaDescription\>
              A responsive modal component for shadcn/ui.
            </CredenzaDescription\>
          </CredenzaHeader\>
          <CredenzaBody\>This modal got triggered using state</CredenzaBody\>
          <CredenzaFooter\>
            <CredenzaClose asChild\>
              <Button\>Close</Button\>
            </CredenzaClose\>
          </CredenzaFooter\>
        </CredenzaContent\>
      </Credenza\>
    </\>
  )
}

Credits
-------

-   shadcn/ui by shadcn
-   Vaul by emilkowalski
