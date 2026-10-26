# CS 350: Emerging Systems Architectures and Technologies

## Portfolio Artifacts

1. **Thermostat.py**: Python code that runs a smart thermostat prototype on a Raspberry Pi 4B. It reads an AHT20 temperature sensor over I2C, handles three buttons with GPIO interrupts, fades red and blue LEDs to show heating and cooling, updates a 16x2 LCD, and sends a status string over UART.
2. **CS350_Final_Project_Report.docx**: A two-page report comparing the Raspberry Pi Pico W, the Microchip WFI32E01, and the NXP Kinetis K64F for the production version of the thermostat, with a recommendation based on peripherals, Wi-Fi, and Flash and RAM.

Supporting file: **Thermostat_StateMachine.pdf**, the state machine diagram for the thermostat.

## Reflection

### Summary of the project and the problem it solved
SysTec wanted to enter the smart thermostat market, and they needed a working prototype of the low-level thermostat behavior before building the Wi-Fi version. I built that prototype. The thermostat has three states (off, heat, and cool). One button cycles through the states, and the other two raise and lower the set point, which starts at 72 degrees Fahrenheit. The LEDs fade when the system is actively heating or cooling and stay solid once the room reaches the set point. Every 30 seconds it sends the state, temperature, and set point over the serial port to simulate sending data to a server. I also wrote a report recommending which hardware architecture SysTec should use for the cloud-connected product.

### What I did particularly well
I think the state machine is the strongest part of my work. Each state has clear entry and exit actions, so the LEDs always end up in the right condition when the state changes. I also tested each feature as I went: the buttons first, then the sensor, then the serial output with the server simulator. That made problems easier to find. In the report, I compared all three architectures against the same three requirements, so the recommendation follows from the evidence instead of from a preference.

### Where I could improve
I need to manage my time better. I turned this project in late, and my first demo video ran a little over the two-minute limit. I also noticed the sensor reading bounces by a few tenths of a degree, and since the code rounds down, an LED can flip between fading and solid when the set point is right at the room temperature. Next time I would add a small buffer or average several readings to make that more stable.

### Tools and resources I am adding to my support network
- SSH and `scp` for working on a remote board
- The gpiozero library and Python state machine library
- draw.io for state diagrams
- Vendor datasheets from Raspberry Pi, Microchip, and NXP
- The server simulator script for testing UART output
- My instructor and the course lab guides for hardware wiring questions

### Skills that transfer to other projects and coursework
Working with I2C, UART, and GPIO transfers to any embedded or IoT project. Designing with a state machine helps with any program that has modes, including games, UI flows, and network protocols. Reading datasheets and comparing hardware against business requirements will help me in system design work and in any role where I have to justify a technical choice.

### How I made the project maintainable, readable, and adaptable
I kept the code organized around one state machine class, with a separate method for each action, such as updating the lights, building the serial string, and handling each button. I used clear names and comments throughout, and a `DEBUG` flag lets me turn console output on or off without changing the logic. Values like the set point, pin numbers, and serial settings are defined in one place, so changing the hardware or behavior means editing a few lines. I also documented the behavior in a state machine diagram, so someone could understand the design without reading the code.
