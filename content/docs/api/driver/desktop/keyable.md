---
layout: page
tags: [api]
title: desktop.Keyable
package: fyne.io/fyne/v2/driver/desktop
---

# desktop.Keyable
---
```go
import "fyne.io/fyne/v2/driver/desktop"
```

## Usage

#### type Keyable

```go
type Keyable interface {
	fyne.Focusable

	KeyDown(*fyne.KeyEvent)
	KeyUp(*fyne.KeyEvent)
}
```

Keyable describes any focusable canvas object that can accept desktop key events. This is the traditional key down and up event that is not applicable to all devices.