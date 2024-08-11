# Stress Analysis MATLAB App

This MATLAB app calculates rotation stresses, shear values, and their associated angles, and generates Mohr's Circle for stress visualization. The app provides an interactive interface for entering stress parameters and viewing results.

## Features

- **Calculate Rotation Stresses**: Computes normal stresses (σx and σy), shear stresses, and their angles.
- **Generate Mohr's Circle**: Visualizes stress transformation.
- **Principal Stresses**: Calculates and displays principal stresses and their angles.
- **Maximum Shear Stress**: Computes and displays maximum shear stress and angles.

## Usage

1. **Input Parameters**:
   - **σx**: Normal stress in the x-direction.
   - **σy**: Normal stress in the y-direction.
   - **τ**: Shear stress.
   - **Rotation Angle**: Angle of rotation in degrees.

2. **Run the App**:
   - Open MATLAB.
   - Run the `.mlapp` file associated with this project.

3. **View Results**:
   - The app calculates and displays:
     - Normal stresses after rotation.
     - Principal stresses and their angles.
     - Maximum shear stress and its angle.
   - Mohr's Circle plot is provided for visualization.

## Equations Used

```matlab
% Inputs
sigma_x = app.sigma_xEditField.Value;
sigma_y = app.sigma_yEditField.Value;
tau = app.ShearEditField.Value;
angle_degrees = app.RotationangleEditField.Value;

angle_radians = deg2rad(angle_degrees);

% Outputs
sigmax1 = sigma_x * cos(angle_radians)^2 + sigma_y * sin(angle_radians)^2 + 2 * tau * sin(angle_radians) * cos(angle_radians);
sigmay1 = (sigma_x + sigma_y) / 2 - ((sigma_x - sigma_y) / 2) * cos(2 * angle_radians) - tau * sin(2 * angle_radians);
tau1 = ((sigma_y - sigma_x) / 2) * sin(2 * angle_radians) + tau * cos(2 * angle_radians);

% Principal Stress
sigma_1 = ((sigma_x + sigma_y) / 2) + sqrt(((sigma_x - sigma_y) / 2)^2 + tau^2);
sigma_2 = ((sigma_x + sigma_y) / 2) - sqrt(((sigma_x - sigma_y) / 2)^2 + tau^2);
theta_p1 = atan2d(2 * tau, sigma_x - sigma_y) / 2;
theta_p2 = theta_p1 + 90;

app.Sigma1EditField.Value = sigma_1;
app.sigma2EditField.Value = sigma_2;
app.thetap1EditField.Value = theta_p1;
app.thetap2EditField.Value = theta_p2;

% Maximum Shear
shear_max = sqrt(((sigma_x - sigma_y) / 2)^2 + tau^2);
app.MaximumShearEditField.Value = shear_max;
shear_angle1 = theta_p1 - 45;
shear_angle2 = theta_p1 + 45;
app.Thetas1EditField.Value = shear_angle1;
app.Thetas2EditField.Value = shear_angle2;

% Angle
slope = (-tau - tau) / (sigma_y - sigma_x);
angle_rad = atan(slope);
angle_deg = rad2deg(angle_rad);
angle_deg_rounded = round(angle_deg, 2);
text(app.UIAxes, xcenter, angle_deg, ['  ∠ to X-axis: ', num2str(angle_deg_rounded), '°']);
```

## Screenshot

![Working app](https://github.com/user-attachments/assets/955b8995-8763-407c-9f76-68d3fbddeab6)
![Working app 2](https://github.com/user-attachments/assets/104ac8c2-7164-4b79-853b-c97b597a52c4)



## License

This project is licensed under the Professional License Agreement. See the [LICENSE.md](LICENSE.md) file for details.
