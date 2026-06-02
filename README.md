# amalgame-hardware-motor

Portable **motor / actuator drivers** for Amalgame over [`amalgame-hal`](https://github.com/amalgame-lang/amalgame-hal): servos/ESCs (drones), steppers (3D printers/CNC), DC motors via H-bridge (robots), relays. One driver, runs on Raspberry Pi and future MCU backends.

```sh
amc package add hardware-motor
```

```amalgame
import Amalgame.Hardware          // Pwm, GpioOut, SysClock (Pi)
import Amalgame.Hardware.Motor

let s = new Servo(new Pwm(0,0))
s.Write(90)                       // degrees (or s.Throttle(50) for an ESC)

let st = new Stepper(new GpioOut(17), new GpioOut(18),
                     new GpioOut(27), new GpioOut(22), new SysClock())
st.Step(2048, 2)                  // 28BYJ-48: ~half a revolution, 2ms/step
```

| Class | API |
|---|---|
| `Servo(pwm)` | `Write(angle 0..180)`, `Throttle(0..100)`, `SetRange(minUs,maxUs)` |
| `DcMotor(in1,in2: DigitalOut, en: PwmOut)` | `Forward(%)` / `Reverse(%)` / `Stop()` / `Brake()` |
| `Stepper(c1..c4: DigitalOut, clk: Clock)` | `Step(count, delayMs)` / `Release()` |
| `Relay(out: DigitalOut)` | `On()` / `Off()` / `Set(on)` / `SetActiveHigh(b)` |

Requires amc ≥ 0.8.72. Apache-2.0.
