#  Mirrorboard for macOS (Karabiner-Elements)

A modern macOS implementation of Randall Munroe’s **XKCD Mirrorboard**:  
a one-handed keyboard layout that mirrors the right-hand side of the keyboard onto the left, allowing comfortable typing with a single hand.

This version is implemented as a **Karabiner-Elements complex modification**, with a focus on:
- left-handed use
- correct handling of modifiers (Shift, Cmd, Option)

---

## Background and inspiration

This project is inspired by Randall Munroe’s original blog post:

> **“Mirrorboard: A One-Handed Keyboard Layout for the Lazy”**  
> https://blog.xkcd.com/2007/08/14/mirrorboard-a-one-handed-keyboard-layout-for-the-lazy/

In the original concept, holding a modifier key turns the keyboard into a mirror image of itself, so that keys normally typed with the right hand can be typed with the left.

This repository brings that idea up to date for **modern macOS** using **Karabiner-Elements**.

---

## What this configuration does

### Mirror mode
- **Hold `Space`** to activate *mirror mode*
- While held, keys on the **left-hand side** output their **right-hand equivalents**
- Release `Space` to return to normal typing
- Tap `Space` normally to insert a space (unchanged behaviour)

This creates a **temporary mirrored layer**, rather than a permanent layout change.

---

## Left-handed mirror mapping (overview)

### Letters
| Left-hand key | Outputs |
|--------------|---------|
| Q W E R T | P O I U Y |
| A S D F G | ; L K J H |
| Z X C V | . , M N |

All letter mappings **pass through modifiers**, so:
- `Shift` produces capitals
- `Cmd`, `Option`, etc. continue to work naturally

---

### Number row
| Left-hand key | Outputs |
|--------------|---------|
| 1 2 3 4 5 | 0 9 8 7 6 |

Modifiers are preserved, so combinations like `Cmd+1` still work as expected.

---

### Punctuation and symbols
- UK keyboard layouts are supported
- The following additional mappings are included:
  - **`§` → `-`** (hyphen)
  - **`` ` / ~ `` → `/`**
- Bottom-row punctuation is mirrored for one-handed access:
  - `Z → .`
  - `X → ,`
  - `C → M`
  - `V → N`

---

### Extra mirror-mode shortcuts
While mirror mode is active:

| Key | Action |
|----|--------|
| `Tab` | Backspace |
| `Caps Lock` | Enter |

These are ergonomic conveniences for one-handed editing.

---

## Installation and configuration

### 1. Install Karabiner-Elements
Download and install from:  
https://karabiner-elements.pqrs.org/

Make sure you allow the system extension in **System Settings → Privacy & Security**, then reboot if prompted.

---

### 2. Install the configuration

1. Copy the JSON file from this repository into:

   ```bash
   ~/.config/karabiner/assets/complex_modifications/
   ```

	2.	Open Karabiner-Elements
	3.	Go to Complex Modifications
	4.	Click Add rule
	5.	Enable “Hold Space to mirror left-hand keys (XKCD Mirrorboard)”

---

### Changing the mirror key

Mirror mode is controlled by this block at the top of the file:
```json
{
  "type": "basic",
  "from": {
    "key_code": "spacebar",
    "modifiers": { "optional": ["any"] }
  },
  "to": [{ "set_variable": { "name": "mirror_mode", "value": 1 } }],
  "to_after_key_up": [
    { "set_variable": { "name": "mirror_mode", "value": 0 } }
  ],
  "to_if_alone": [{ "key_code": "spacebar" }]
}
```

### To use a different mirror key

Change "key_code": "spacebar" to another key, for example:
- "caps_lock"
- "right_command"
- "fn" (Globe key)
- "left_control"

If you change the mirror key, you may also want to remove or adjust to_if_alone.

---
### Keyboard layouts

- This configuration is written with UK keyboards in mind
- It should work on US keyboards with minor tweaks (notably around non_us_backslash and symbol placement)
- Use Karabiner → EventViewer to confirm key codes on your layout


---

### Licence

This configuration is released under the MIT License.
You are free to use, modify, and redistribute it.

---

### Acknowledgements

- Randall Munroe (XKCD) for the original Mirrorboard idea
- The Karabiner-Elements project and community

---

Enjoy one-handed typing ✨
Pull requests and adaptations welcome.
