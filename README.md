# Motion Detection and Segmentation

This repository contains a Python project for detecting and segmenting motion ranges from CSV files containing angle data. The code processes CSV files with angle measurements (e.g., shoulder, elbow, wrist angles) and timestamps, then segments the motion based on defined thresholds and criteria. Segmented motion ranges are saved as new CSV files and visualized through plots.

## How It Works

1. **Data Input**  
   - CSV files are expected in the `MovementData` folder.
   - Each CSV should include columns for angle measurements (e.g., `right_elbow_angle`, `left_shoulder_angle`) and an elapsed time column (`elapsed_time`).

2. **Settings and Thresholds**  
   - The code uses adjustable settings (defined in the *Settings* section) to determine when a movement range begins and ends.
   - **Detection Settings:**  
     - `exceed_threshold`: The threshold for an angle to exceed the current zone, triggering a state change.  
     - `exceed_frame_required`: The number of consecutive frames that must exceed the threshold.
   - **Local Maxima/Minima Settings:**  
     - `abduction_height`, `shoulder_flexion_height`, and `elbow_flexion_height` are used to detect local extrema in the data.
   - **Folder and CSV Settings:**  
     - Input CSV files are read from the `MovementData` folder.
     - Segmented motion results and plots are saved in the `SegmentedMotion` folder.
   - **Angle Headers:**  
     - Predefined CSV headers for different angles (e.g., elbow, shoulder, wrist) are available for processing.

3. **Motion Segmentation Process**  
   - The project contains functions that:
     - **Unwrap angles:** A basic unwrapping function is provided.
     - **Segment Motion:** Functions `GetMovementRangeFromAngleData_Narrow` and `GetMovementRangeFromAngleData_Wide` detect motion ranges using different thresholds (depending on the posture type).
     - **Plotting:** The `plot_data_with_elapsed_timestamp` function plots the raw and segmented data along with detected local extrema.
   - After processing, segmented motion ranges are saved as new CSV files, and corresponding plots are generated.

4. **Output**  
   - The final output includes segmented CSV files and plots saved under `SegmentedMotion/[filename]/` for each processed file.

## File Naming Requirements

For the processing script to correctly identify the posture and side from the CSV filenames, **each file must include**:
- **An exact posture name:** One of `Abduction`, `ShoulderFlexion`, or `ElbowFlexion`.
- **An exact side:** Either `left` or `right` (case-insensitive).

For example, valid filenames might include:
- `Subject1_ShoulderFlexion_right.csv`
- `Subject2_ElbowFlexion_left.csv`

If a file does not include one of the required posture names or side indicators, the script will raise an error and halt processing.

## Settings You Can Adjust

- **Detection and Segmentation Settings:**
  - `exceed_threshold`: Adjust this to change the sensitivity of state transitions.
  - `exceed_frame_required`: Modify the number of consecutive frames required to trigger a state change.
  
- **Local Maxima and Minima Settings:**
  - `abduction_height`: Set the height for detecting local minima for abduction.
  - `shoulder_flexion_height`: Set the height for detecting local minima for shoulder flexion.
  - `elbow_flexion_height`: Set the height for detecting local maxima for elbow flexion.

- **Folder Settings:**
  - `csv_saved_folder_path`: Change the folder name where your input CSV files are stored.
  - `pose_movement_folder_path`: Change the folder name where the segmented motion results will be saved.

- **CSV Headers:**
  - Adjust the CSV header names if your CSV files have different column names (e.g., for different angles or timestamps).

- **Plotting Settings:**
  - `angle_spacing`: Change the step size for the y-axis ticks.
  - `plot_font_sizes`: Modify font sizes for titles, labels, legends, and ticks for better visualization.

## Installation

Make sure you have Python installed. Then install the necessary dependencies:

```bash
pip install numpy pandas matplotlib scipy
```

Alternatively, if you have a `requirements.txt` file, run:

```bash
pip install -r requirements.txt
```

## How to Run

1. **Prepare Your Data:**  
   Place your CSV files with the required angle and timestamp data into the `MovementData` folder. Ensure that each filename contains one of the required posture names and a side (left/right).

2. **Run the Script:**  
   Execute the main Python script (e.g., `python main.py`). The script will:
   - Read each CSV file,
   - Process the data to segment motion ranges,
   - Save the segmented data and plots in the `SegmentedMotion` folder.

3. **Review the Output:**  
   Check the generated CSV files and plots in the `SegmentedMotion` folder to analyze the segmented motion data.

## Contributing

Contributions and suggestions are welcome! Feel free to open an issue or submit a pull request if you have ideas for improving the code or documentation.

## License

[MIT License](LICENSE)
