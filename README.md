import time
import random
from datetime import datetime

# -----------------------------
# CONFIGURATION
# -----------------------------
VOLTAGE = 230          # AC voltage (Volts)
POWER_THRESHOLD = 100  # Watts (limit for wastage detection)
CHECK_INTERVAL = 5     # seconds

LOG_FILE = "energy_log.txt"

# -----------------------------
# SENSOR READING (SIMULATION)
# Replace this with real sensor code
# -----------------------------
def read_current_sensor():
    """
    Simulates current sensor reading.
    Replace with actual ADC/sensor code.
    """
    current = round(random.uniform(0.1, 1.5), 2)  # Amps
    return current

# -----------------------------
# POWER CALCULATION
# -----------------------------
def calculate_power(voltage, current):
    return round(voltage * current, 2)

# -----------------------------
# LOG DATA
# -----------------------------
def log_data(current, power):
    with open(LOG_FILE, "a") as file:
        file.write(f"{datetime.now()} | Current: {current} A | Power: {power} W\n")

# -----------------------------
# NOTIFICATION FUNCTION
# -----------------------------
def send_notification(power):
    print("⚠ ALERT: ENERGY WASTAGE DETECTED!")
    print(f"⚡ Power Consumption: {power} Watts")
    print("📩 Notification sent to user\n")

# -----------------------------
# MAIN FUNCTION
# -----------------------------
def main():
    print("IoT Based Energy Wastage Detection System Started...\n")

    while True:
        current = read_current_sensor()
        power = calculate_power(VOLTAGE, current)

        print(f"Current: {current} A | Power: {power} W")
        log_data(current, power)

        if power > POWER_THRESHOLD:
            send_notification(power)

        time.sleep(CHECK_INTERVAL)

# -----------------------------
# PROGRAM START
# -----------------------------
if __name__ == "__main__":
    main()
