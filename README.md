# Training Load Data Field

A Garmin Connect IQ data field that calculates and displays your real-time training load during activities using the TRIMP (Training Impulse) method.

<img width="282" height="426" alt="Screenshot 2026-02-10 at 17 16 19" src="https://github.com/user-attachments/assets/8f87a309-e7f3-4c05-a4db-c79c02694cf2" />

## Installation

1. Find & Download the `TrainingLoadField.prg` App for your device from the [Releases](../../releases) page
2. Connect your Garmin watch to your computer via USB
3. Copy the App to the `GARMIN/APPS` folder on your watch
4. Safely eject your watch

## Usage

1. On your Garmin watch, go to an activity (e.g., Run, Bike, etc.)
2. Long press to access activity settings
3. Navigate to **Data Screens** → **Add Data Field**
4. Select **Training Load** from the Connect IQ data fields
5. Start your activity - the field will display your accumulating training load in real-time

## How It Works

### TRIMP Calculation

The data field uses an exponential heart rate-based formula to calculate training load, this method gives more weight to high-intensity efforts, reflecting the greater physiological stress they cause.

### Data Storage

- Training load is saved when you stop or end an activity
- Data is stored in shared application storage with a 7-day rolling history
- Multiple activities on the same day are accumulated together

### Companion Widget

This data field shares data with the **Training Load Widget**. 
After your workouts, the widget displays:
- 7-day total training load
- Training status (Low, Recovery, Maintaining, Optimal, High, Overreaching)
- Visual load indicator bar

### Understanding the Numbers

| 7-Day Total | Status |
|-------------|--------|
| 0-150 | Low |
| 150-400 | Recovery |
| 400-700 | Maintaining |
| 700-1000 | Optimal |
| 1000-1300 | High |
| 1300+ | Overreaching |

*Note: Values vary based on individual fitness and workout duration*

## Supported Devices

- **Forerunner**: 55, 165, 165M, 255 series, 265 series, 955, 965
- **Fenix**: 5 series, 6 series, 7 series (including Pro variants)
- **Epix**: Gen 2, Pro (42mm, 47mm, 51mm)
- **Venu**: Original, 2 series, 3 series, Sq series
- **Vivoactive**: 3 series, 4 series, 5
- **Enduro**: Original
- **Instinct**: 2 series, Crossover
- **Descent**: Mk2, Mk2s
- **MARQ**: All variants (Gen 1 & 2)
- **D2**: Air X10, Mach 1
- **Approach**: S70 (42mm, 47mm)

## Permissions

- **Sensor**: Required to access heart rate data
- **UserProfile**: Required to read max HR and resting HR from your profile

## License

MIT License - See LICENSE file for details

