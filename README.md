# StormShield: Hurricane Patient Evacuation Optimization Model

**StormShield** is an advanced integer programming-based optimization framework designed to enhance patient evacuation strategies during hurricanes, particularly for ICU patients in Florida. By leveraging data-driven insights including FEMA's National Risk Index, it balances patient safety, environmental impact, and cost-effectiveness. With StormShield, decision-makers can shift from reactive, last-minute evacuations to proactive, well-structured plans that minimize healthcare disruptions and save lives.

## 🎯 Project Overview

This project addresses the critical challenge of evacuating patients from high-risk hospitals during hurricane events in Florida. The model optimizes the allocation of emergency medical services (EMS) vehicles to efficiently transport patients from high-risk to safe hospitals while considering multiple objectives:

- **Maximize patient evacuation** (highest priority)
- **Minimize environmental pollution** (medium priority) 
- **Minimize operational costs** (lower priority)

## 📊 Key Results

The optimization model successfully generated an evacuation plan with the following outcomes:

| Metric | Value |
|--------|-------|
| **Total Patients Evacuated** | 4,597 |
| **Total Cost** | $756,560.07 |
| **Total Pollution** | 1,518,528.62 pounds of CO₂ |
| **Maximum Evacuation Time** | 96 hours (4 days) |

### Vehicle Utilization Breakdown:
- **Ambulances**: 177 vehicles → 1,609 patients
- **Air Ambulances**: 32 vehicles → 32 patients  
- **Fire Ambulances**: 128 vehicles → 1,196 patients
- **Buses**: 19 vehicles → 1,760 patients

## 🏥 Data Sources & Processing

### Datasets Used:
1. **EMS Dataset**: Contains information about emergency medical services stations including:
   - Location data (coordinates, county)
   - Vehicle fleet information (ambulances, air ambulances, fire ambulances, buses)
   - Facility type and population served

2. **Hospital Dataset**: Includes details about hospitals in the region:
   - Location and capacity information
   - ICU patient counts
   - Bed availability and vacancy rates

3. **Hurricane Dataset**: Provides hurricane risk information:
   - FEMA's National Risk Index data
   - Hurricane frequency and risk scores by county

### Data Processing:
- **Geographical Filtering**: Applied Florida boundary constraints (24.396308°N to 31.000888°N, -87.634938°W to -80.031362°W)
- **Risk Classification**: Hospitals classified as high-risk (≥98.0 risk score) or safe (<98.0 risk score)
- **Distance Calculations**: Used Haversine formula for accurate distance computations between locations

## 🚗 Vehicle Parameters

### Vehicle Types & Capacities:
- **Ambulance**: 2 patients, 55 mph, 4.9 MPG
- **Air Ambulance**: 1 patient, 160 mph, 39.63 gal/hour
- **Fire Ambulance**: 2 patients, 55 mph, 4.9 MPG  
- **Bus**: 20 patients, 40 mph, 7.0 MPG

### Operational Parameters:
- **Utilization Factor**: 50% of each vehicle type available for evacuation
- **Turnaround Time**: 30 minutes for ground vehicles, 1 hour for air ambulances
- **Staff Requirements**: 2 paramedics for ground vehicles, 1 pilot + 1 paramedic for air ambulances

## 🧮 Optimization Model

### Mathematical Formulation:
The model uses Gurobi optimization solver with the following key components:

#### Decision Variables:
- `u[e,r,v]`: Number of vehicles of type v from EMS station e to risky hospital r
- `x[r,s,v]`: Number of round trips by vehicle type v from risky hospital r to safe hospital s
- `z[r,s,v]`: Number of round trips made by vehicle type v from risky hospital r to safe hospital s

#### Key Constraints:
1. **Vehicle Capacity Limits**: EMS station vehicle availability constraints
2. **Flow Balance**: Conservation of vehicles between EMS stations and hospitals
3. **Time Constraints**: Maximum 96-hour evacuation window
4. **Patient Evacuation**: All ICU patients must be evacuated
5. **Safe Hospital Capacity**: Respecting destination hospital capacity limits

#### Multi-Objective Function:
1. **Primary**: Maximize number of evacuated patients
2. **Secondary**: Minimize environmental pollution (CO₂ emissions)
3. **Tertiary**: Minimize total operational costs

## 🛠️ Technical Implementation

### Dependencies:
- **Python 3.x**
- **Gurobi Optimization Solver**
- **Pandas** for data manipulation
- **NumPy** for numerical computations
- **Matplotlib** and **Plotly** for visualization
- **NetworkX** for network analysis
- **Basemap** for geographical plotting

### Key Functions:
- `calculate_distance()`: Haversine distance calculation
- `is_in_florida()`: Geographical boundary filtering
- Multi-objective optimization setup with Gurobi
- Comprehensive visualization suite

## 📈 Visualizations & Analysis

The notebook includes extensive visualizations:

1. **Geographical Maps**: Florida hospital distribution (high-risk vs safe)
2. **Evacuation Routes**: Network visualization of optimal routes by vehicle type
3. **Performance Metrics**: Cost vs pollution vs people transported analysis
4. **Time Analysis**: Evacuation time distributions and cumulative progress
5. **Resource Allocation**: Top EMS stations and hospital vehicle distributions

## 🚀 Getting Started

### Prerequisites:
1. Install Python 3.x
2. Install Gurobi optimization solver
3. Install required Python packages:
   ```bash
   pip install pandas numpy gurobipy matplotlib plotly networkx basemap seaborn tabulate
   ```

### Running the Model:
1. Ensure all dataset files are in the project directory:
   - `EMS_Dataset_Final1.csv`
   - `Hospital_Dataset_Final1.csv` 
   - `Hurican_dataset.csv`
2. Open and run `Optimization_code.ipynb` in Jupyter Notebook
3. The model will automatically process data, run optimization, and generate results

## 📚 Documentation

For detailed information about the model and its implementation, please refer to:
- **Technical Documentation**: `Stormsheild_Hurricane_evacuation_optimization_model.pdf`
- **Project Presentation**: `MGSC_662-Stormsheild_model_presentation.pdf`

## 🎓 Academic Context

This project was developed as part of MGSC 662 coursework, demonstrating advanced optimization techniques applied to real-world emergency management scenarios. The model showcases the practical application of integer programming in disaster response planning.

## 🔬 Methodology Highlights

- **Multi-Objective Optimization**: Balances humanitarian, environmental, and economic objectives
- **Real-World Data Integration**: Uses actual Florida hospital and EMS data
- **Geographical Precision**: Accounts for Florida's specific geography and hurricane patterns
- **Comprehensive Analysis**: Includes cost, pollution, and efficiency metrics
- **Scalable Framework**: Can be adapted for other regions and disaster scenarios

## 📞 Contact & Support

For questions about the model implementation or optimization methodology, please refer to the technical documentation or project presentation materials included in this repository.
