# King County Housing Market Analysis & Price Prediction

## Project Overview

This project analyzes the King County, Washington real estate market using machine learning to predict house prices and understand the key factors driving the housing market. Using over 21,000 house sales transactions from 2014-2015, the analysis explores spatial pricing patterns, property value determinants, and market trends across the region.

**Key Objectives:**
- Build regression models to predict house prices accurately
- Identify key factors influencing property values in King County
- Analyze spatial and geographic pricing patterns
- Generate insights for buyers, sellers, investors, and policy makers
- Understand market dynamics through data visualization

## Problem Statement

The King County real estate market is complex and dynamic, with significant price variations across neighborhoods and property types. Understanding what drives house prices is valuable for making informed pricing decisions, investment strategies, and housing policy analysis. This project applies data science to decode housing market mechanisms.

## Dataset

**Data Source:** King County Housing Transaction Records (2014-2015)

**Dataset Size:**
- **Total Records:** 21,060 house sales transactions
- **Time Period:** October 2014 - December 2015
- **Geographic Coverage:** King County, Washington (includes Seattle and surrounding areas)
- **Data Quality:** No missing values across all features

**Features (16 variables):**
| Feature | Type | Range | Description |
|---------|------|-------|-------------|
| `price` | Numeric | $75K - $1.495M | Sale price (target variable) |
| `sqft_living` | Numeric | 290 - 7,480 sq ft | Square footage of living space |
| `sqft_lot` | Numeric | 520 - 1,651,359 sq ft | Total lot size |
| `bedrooms` | Integer | 0 - 7 | Number of bedrooms |
| `bathrooms` | Float | 0 - 6.75 | Number of bathrooms |
| `floors` | Float | 1 - 3.5 | Number of floors |
| `waterfront` | Categorical | Yes/No | Waterfront property indicator |
| `view` | Categorical | Various | View quality (No View, Fair, Good, Excellent) |
| `condition` | Categorical | Poor to Very Good | Property condition rating |
| `grade` | Integer | 1 - 12 | Construction quality grade |
| `yr_built` | Integer | 1900 - 2015 | Year property was built |
| `zipcode` | Integer | 98001 - 98199 | ZIP code (geographic identifier) |
| `lat` / `long` | Float | Geographic coordinates | Latitude and longitude |
| `date` | Datetime | Oct 2014 - Dec 2015 | Sale date |

**Data Statistics:**
- **Average Price:** $500,270
- **Median Price:** $445,000
- **Price Std Dev:** $246,578
- **Most Common:** 3 bedrooms, 2.25 bathrooms, built 1975
- **Most Recent:** Properties built up to 2015

## Methodology

**Data Exploration & Preprocessing:**
- Temporal analysis of sales dates
- Geographic distribution analysis (latitude/longitude, ZIP code patterns)
- Feature correlation and multicollinearity assessment
- Outlier detection and handling
- Feature scaling and encoding of categorical variables

**Models Implemented:**
- **Linear Regression** (baseline model for interpretability)
- **Ridge Regression** (handles multicollinearity from location features)
- **Lasso Regression** (feature selection)
- **Random Forest** (captures non-linear relationships, feature importance)
- **Gradient Boosting** (enhanced prediction accuracy)

**Key Features Explored:**
- Spatial features (latitude, longitude, ZIP code)
- Property characteristics (bedrooms, bathrooms, square footage)
- Property quality (grade, condition, year built)
- Amenities (waterfront, view)

**Evaluation Metrics:**
- R² Score (coefficient of determination)
- RMSE - Root Mean Square Error
- MAE - Mean Absolute Error
- Cross-validation (k-fold validation)
- Residual analysis

## Key Results

**Model Performance:** [*Add your best model results here, e.g.:*]
- Random Forest: R² = 0.87, RMSE = $127,500
- Gradient Boosting: R² = 0.89, RMSE = $115,300

**Top Price Predictors (by feature importance):**
1. **Square Footage (Living Space)** - Strongest price driver
2. **Location/ZIP Code** - Significant geographic price variation
3. **Grade (Quality)** - Construction quality strongly impacts value
4. **Waterfront Status** - Waterfront properties command premium
5. **Year Built** - Newer properties worth more (controlling for quality)
6. **Number of Bedrooms/Bathrooms** - Moderate impact
7. **View Quality** - Properties with views valued higher

**Geographic Insights:**
- Significant price variation across ZIP codes (geographic clustering visible in dashboard)
- Waterfront and high-view properties in certain areas command 20-40% premiums
- Newer suburbs show price appreciation patterns

**Distribution Patterns:**
- Price distribution is right-skewed (long tail of luxury properties)
- Bedroom distribution: Most homes have 3-4 bedrooms (majority of market)
- Bathroom distribution: Concentrated around 1.5-2.5 bathrooms
- Strong correlation between living space and price

## Visualizations

The analysis includes interactive Tableau dashboards with:
- **Daily Average House Price** over time (trend analysis)
- **Interactive Map** showing geographic price distribution across King County
- **Distribution of House Prices** (histogram with filters)
- **View vs Condition Heatmap** (price by property attributes)
- **Distribution of Bedrooms & Bathrooms**
- **Filters:** Month/Date, Year Built (1900-2015), Square Footage, etc.

## Usage

```bash
# Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn

# Load and explore data
python src/explore_data.py

# Train models
python src/train_models.py

# Make predictions on new data
python src/predict_price.py --bedrooms 4 --bathrooms 2.5 --sqft_living 2500 --zipcode 98004

# Generate visualizations
python src/visualize_analysis.py

# Fairness audit
python src/audit_fairness.py
```

## Limitations & Future Work

**Current Limitations:**
- Training data limited to 2014-2015 period - market conditions have evolved significantly
- Geographic scope: King County only (Seattle metro area) - results may not generalize to other markets
- Limited incorporation of neighborhood amenities (schools, parks, walkability, public transit)
- No consideration of external factors (interest rates, economic indicators, school quality)
- Property maintenance history and renovation status not available
- Model captures historical pricing patterns, including any embedded biases

**Future Enhancements:**
- Time series modeling to account for market trends and seasonality
- Integration of neighborhood-level features (school districts, crime rates, walkability scores)
- Dynamic pricing models that adjust for market conditions
- Causal inference to distinguish correlation from causation
- Address-level data for fine-grained spatial analysis
- Incorporate non-traditional features (property photos, listing descriptions via NLP)

---

## 🚨 Ethical Considerations

### 1. **Fair Housing & Discrimination Risk**
   - **Risk:** Pricing models may perpetuate or amplify historical housing discrimination based on race, ethnicity, national origin, or disability status.
   - **How it happens:**
     - Properties in historically redlined neighborhoods (often areas with higher concentrations of minority residents) may receive systematically lower valuations
     - ZIP code or latitude/longitude may serve as proxies for protected characteristics
     - Historical property values embedded in training data reflect past discrimination
     - Appraisers could use model predictions to justify discriminatory pricing
   
   - **Ethical Concerns:**
     - Fair housing laws (Fair Housing Act) prohibit discrimination in housing transactions
     - Algorithmic pricing that perpetuates discrimination is illegal, even if unintentional
     - "Objective" algorithmic recommendations can obscure and legitimize discrimination
   
   - **Our Mitigation:**
     - ✅ Audit model predictions across neighborhoods with different racial/ethnic demographics
     - ✅ Test for disparate impact: Do identical properties receive different predicted prices in different neighborhoods?
     - ✅ Analyze residuals (prediction errors) by geographic area to identify systematic bias
     - ✅ Compare model predictions to actual appraisals to detect discrimination patterns
     - ✅ Remove or carefully evaluate location variables that proxy for protected characteristics
     - ✅ Document historical biases in the data explicitly
   
   - **Transparency:**
     - Disclose known geographic biases in model predictions
     - Make clear that model reflects historical market patterns, including past discrimination
     - Provide explainability for property-level predictions so appraisers can challenge algorithmic recommendations

### 2. **Housing Affordability & Market Gentrification Impact**
   - **Risk:** Accurate pricing models can be weaponized to extract maximum value from properties, potentially:
     - Accelerating gentrification and displacement of long-time residents
     - Enabling speculative investment in affordable housing
     - Contributing to rising housing costs and affordability crises
     - Displacing communities and destroying neighborhood social fabric
   
   - **Ethical Questions:**
     - Should we optimize for maximum profit, or consider community impact?
     - Does improving pricing accuracy contribute to housing affordability crises?
     - What responsibility do data scientists have for downstream societal effects?
   
   - **Considerations:**
     - Be aware of downstream impacts of pricing accuracy improvements
     - Consider recommending fair and equitable pricing approaches alongside profit-maximizing ones
     - Engage with housing equity discussions and community stakeholders
     - Recognize that "market-rate" pricing may not be ethical pricing
   
   - **Accountability:**
     - ✅ Monitor actual use of model to detect speculative or discriminatory pricing
     - ✅ Recommend transparency in pricing to prevent predatory practices
     - ✅ Engage with community organizations working on housing affordability
     - ✅ Consider impact on vulnerable populations (elderly, low-income, communities of color)

### 3. **Data Privacy & Property Owner Information**
   - **Risk:** Housing transaction data reveals sensitive personal information:
     - Financial status and net worth
     - Family composition and life events (marriage, divorce, death)
     - Health status (accessibility modifications, long-term care facilities nearby)
     - Lifestyle and preferences (waterfront, views, property upgrades)
   
   - **Privacy Concerns:**
     - De-anonymization: Properties with unique features can be identified (e.g., "only waterfront property in ZIP 98001")
     - Linking with other datasets could reveal sensitive information
     - Data breaches could expose personal financial information
   
   - **Best Practices:**
     - ✅ Minimize collection of sensitive personal information beyond transaction data
     - ✅ De-identify owner names and contact information
     - ✅ Comply with data protection laws (privacy regulations)
     - ✅ Secure data storage and access controls
     - ✅ Clear data retention and deletion policies
     - ✅ Consider obtaining owner consent for data use

### 4. **Appraisal Bias & Legitimacy Concerns**
   - **Risk:** Algorithmic predictions may be misused as "objective" justification for biased appraisals.
   - **Example:** A model predicting lower prices in a specific neighborhood could legitimize discriminatory appraisals if:
     - The model is based on biased historical data
     - Lower valuations reflect discrimination, not true market conditions
     - Appraisers treat algorithm as authoritative rather than one input among many
   
   - **Mitigation:**
     - ✅ Acknowledge that models reflect historical market patterns, **including discrimination**
     - ✅ Recommend professional appraisers review and challenge algorithm recommendations
     - ✅ Use model as one input among many, not as definitive truth
     - ✅ Build in explainability so appraisers understand assumptions and can override predictions
     - ✅ Require human judgment for final appraisals, especially in marginalized communities
     - ✅ Document cases where algorithm disagrees with fair market value

### 5. **Model Representativeness & Market Segments**
   - **Risk:** Model may not apply equally across all property types and market segments.
   - **Limitations:**
     - Luxury properties may be underrepresented (fewer transactions)
     - New construction (2015+) not represented in training data
     - Properties with unique characteristics may have unreliable predictions
     - Market has evolved significantly since 2014-2015
   
   - **Best Practices:**
     - ✅ Test model performance separately across property segments (price ranges, property types)
     - ✅ Document which market segments the model applies to
     - ✅ Provide confidence intervals and uncertainty estimates, not point predictions
     - ✅ Explicitly warn against extrapolation beyond training data
     - ✅ Acknowledge temporal limitations (2014-2015 data, market has changed)
     - ✅ Recommend retraining with recent data periodically

### 6. **Responsible Use & Accountability**
   - **Question:** Who is responsible if the model is misused for discrimination or harm?
   - **Framework:**
     - Data scientists have responsibility for known limitations and potential misuses
     - Organizations deploying the model are responsible for fair application
     - Regulatory bodies (HUD, FTC) can enforce fair housing laws
   
   - **Recommended Actions:**
     - ✅ Document model limitations and known biases prominently
     - ✅ Provide clear guidance on fair and responsible use
     - ✅ Include warnings about discrimination risk and regulatory requirements
     - ✅ Consider licensing or access controls to prevent harmful applications
     - ✅ Create audit trail for accountability if discrimination occurs
     - ✅ Be willing to modify or retire models if evidence of discriminatory impact emerges

---

## 📊 Summary of Ethical Commitments

This project is committed to:
- **Fairness:** Regular audits for disparate impact across demographics and geographies
- **Transparency:** Clear documentation of limitations, biases, and assumptions
- **Accountability:** Responsibility for known risks and harmful applications
- **Privacy:** Protection of sensitive homeowner and transaction information
- **Community Impact:** Consideration of effects on housing affordability and neighborhood stability

## Contributing

If you find issues with bias, fairness, or privacy in this analysis, please report them immediately.

## License

[Your License]

---

**Author:** Despi Kotsidou  
**Contact:** dkotsidou@gmail.com  
**Last Updated:** [Date]
