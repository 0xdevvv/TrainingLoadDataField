# Training Load Data Field

A Garmin Connect IQ data field that calculates and displays your real-time training load during activities using the TRIMP (Training Impulse) method.

## Purpose

This data field tracks your training intensity during workouts by calculating a training load score based on your heart rate. It works as a companion to the [Training Load Widget](../TrainingLoad), sharing data so you can view your 7-day training load summary at a glance.

## How It Works

### TRIMP Calculation

The data field uses an exponential heart rate-based formula to calculate training load:

1. **Heart Rate Reserve (HRR)**: Uses your max HR and resting HR from your Garmin user profile
2. **HR Fraction**: `(Current HR - Resting HR) / (Max HR - Resting HR)`
3. **Exponential Weight**: `1.92 × e^(1.92 × HR Fraction)` - Higher heart rates contribute exponentially more to load
4. **Load Increment**: Calculated every second based on time spent at each heart rate

This method gives more weight to high-intensity efforts, reflecting the greater physiological stress they cause.

### Data Storage

- Training load is saved when you stop or end an activity
- Data is stored in shared application storage with a 7-day rolling history
- Multiple activities on the same day are accumulated together

### Companion Widget

This data field shares its UUID with the Training Load Widget, allowing both apps to access the same stored data. After your workouts, the widget displays:
- 7-day total training load
- Training status (Low, Recovery, Maintaining, Optimal, High, Overreaching)
- Visual load indicator bar

## Installation

Since this data field shares a UUID with the Training Load Widget (for data sharing purposes), it cannot be published separately to the Garmin Connect IQ Store. You must sideload it manually.

### Prerequisites

- [Garmin Connect IQ SDK](https://developer.garmin.com/connect-iq/sdk/)
- A compatible Garmin watch (see supported devices below)

### Build & Install

1. Clone this repository
2. Open a terminal in the `TrainingLoadField` directory
3. Build the project:
   ```bash
   # Using the SDK compiler (adjust path to your SDK location)
   monkeyc -d <your_device_id> -f monkey.jungle -o bin/TrainingLoadField.prg -y /path/to/developer_key.der
   ```
   Or use the provided build script:
   ```bash
   ./build.sh
   ```
4. Connect your Garmin watch to your computer
5. Copy `bin/TrainingLoadField.prg` to the `GARMIN/APPS` folder on your watch

### Alternative: Using VS Code

1. Install the [Monkey C extension](https://marketplace.visualstudio.com/items?itemName=garmin.monkey-c) for VS Code
2. Open the `TrainingLoadField` folder
3. Press `Ctrl+Shift+P` → "Monkey C: Build for Device"
4. Select your device and build

## Usage

1. On your Garmin watch, go to an activity (e.g., Run, Bike, etc.)
2. Long press to access activity settings
3. Navigate to **Data Screens** → **Add Data Field**
4. Select **Training Load** from the Connect IQ data fields
5. Start your activity - the field will display your accumulating training load in real-time

### Understanding the Numbers

| Load Value | Typical Effort |
|------------|----------------|
| 0-50 | Light/Easy workout |
| 50-100 | Moderate workout |
| 100-200 | Hard workout |
| 200+ | Very intense/long workout |

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

## Technical Details

- **App Type**: Data Field
- **Min SDK Version**: 3.0.0
- **Language**: Monkey C
- **Shared UUID**: `63EADDDA-5141-4203-A5F5-0AD3A1299A12` (shared with Training Load Widget)

## Related Projects

- [Training Load Widget](../TrainingLoad) - Companion widget that displays your 7-day training load summary

## License

MIT License - See LICENSE file for details

