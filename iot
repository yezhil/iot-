import streamlit as st
import numpy as np
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer
from reportlab.lib.styles import getSampleStyleSheet
from io import BytesIO

# -----------------------
# LOGIN SYSTEM
# -----------------------
if "logged_in" not in st.session_state:
    st.session_state.logged_in = False

def login():
    st.title("🔐 Login - Virtual IoT Lab")
    st.markdown("### Welcome! Please login to continue")

    username = st.text_input("Username")
    password = st.text_input("Password", type="password")

    if st.button("Login"):
        if username == "admin" and password == "1234":
            st.session_state.logged_in = True
            st.rerun()
        else:
            st.error("Invalid credentials ❌")

def logout():
    st.session_state.logged_in = False
    st.rerun()

if not st.session_state.logged_in:
    login()
    st.stop()

# -----------------------
# MAIN APP
# -----------------------
st.set_page_config(page_title="Virtual IoT Sensor Lab", layout="wide")

st.title("🌐 Virtual IoT Sensor Laboratory")

st.sidebar.success("Logged in ✅")
if st.sidebar.button("Logout"):
    logout()

# -----------------------
# PDF generator
# -----------------------
def generate_pdf(title, aim, materials, theory, procedure, observation, result, conclusion, applications):

    buffer = BytesIO()
    styles = getSampleStyleSheet()
    elements = []

    def add_section(title, content):
        elements.append(Paragraph(f"<b>{title}</b>", styles['Heading2']))
        elements.append(Spacer(1, 10))
        elements.append(Paragraph(content, styles['Normal']))
        elements.append(Spacer(1, 15))

    elements.append(Paragraph(f"<b>{title}</b>", styles['Title']))
    elements.append(Spacer(1, 20))

    add_section("Aim", aim)
    add_section("Materials Required", materials)
    add_section("Theory", theory)
    add_section("Procedure", procedure)
    add_section("Observation", observation)
    add_section("Result", result)
    add_section("Conclusion", conclusion)
    add_section("Applications", applications)

    pdf = SimpleDocTemplate(buffer)
    pdf.build(elements)
    buffer.seek(0)
    return buffer

# Sidebar
lab = st.sidebar.selectbox(
    "Select Experiment",
    ["Temperature Sensor", "Soil Moisture Sensor", "Humidity Sensor"]
)

# =======================
# TEMPERATURE SENSOR
# =======================
if lab == "Temperature Sensor":

    st.header("🌡 Temperature Sensor Experiment")

    aim = "To study temperature monitoring using IoT sensors."
    materials = "DHT11 Sensor, Arduino, Breadboard, Jumper wires, Power supply"
    theory = "Temperature sensors convert heat into electrical signals used in IoT systems."
    procedure = """1. Connect sensor to Arduino
2. Power the circuit
3. Read values
4. Display in app"""

    st.subheader("Aim")
    st.write(aim)

    st.subheader("Materials Required")
    st.write(materials)

    st.subheader("Theory")
    st.write(theory)

    st.subheader("Procedure")
    st.write(procedure)

    temp = st.slider("Temperature (°C)", -10, 50, 25)

    if temp > 35:
        result = "High Temperature Detected"
        st.error(result)
    elif temp < 10:
        result = "Low Temperature Detected"
        st.warning(result)
    else:
        result = "Normal Temperature"
        st.success(result)

    observation = "Temperature varies dynamically."
    conclusion = "IoT enables real-time monitoring."
    applications = "Weather, Smart homes, Industry"

    st.subheader("Observation")
    st.write(observation)

    st.subheader("Result")
    st.write(result)

    st.subheader("Conclusion")
    st.write(conclusion)

    st.subheader("Applications")
    st.write(applications)

    data = np.random.randn(20).cumsum() + temp
    st.line_chart(data)

    # Quiz
    st.subheader("🧠 Quiz")
    q = st.radio("Which sensor is used?",
                 ["LDR", "DHT11", "MQ2"], key="tq")

    if st.button("Submit Quiz", key="tbtn"):
        if q == "DHT11":
            st.success("Correct ✅")
        else:
            st.error("Wrong ❌")

    pdf = generate_pdf("Temperature Sensor", aim, materials, theory,
                       procedure, observation, result, conclusion, applications)

    st.download_button("📄 Download Report", pdf, "temperature.pdf")

# =======================
# SOIL SENSOR
# =======================
elif lab == "Soil Moisture Sensor":

    st.header("🌱 Soil Moisture Sensor")

    aim = "To study soil moisture monitoring."
    materials = "Soil Sensor, Arduino, Breadboard, Wires"
    theory = "Measures water content in soil for irrigation systems."
    procedure = """1. Insert sensor in soil
2. Connect to Arduino
3. Read values"""

    st.subheader("Aim")
    st.write(aim)

    st.subheader("Materials Required")
    st.write(materials)

    st.subheader("Theory")
    st.write(theory)

    st.subheader("Procedure")
    st.write(procedure)

    moisture = st.slider("Moisture (%)", 0, 100, 40)

    if moisture < 30:
        result = "Irrigation Required"
        st.error(result)
    else:
        result = "Moisture Normal"
        st.success(result)

    observation = "Moisture changes with soil condition."
    conclusion = "Helps in smart irrigation."
    applications = "Agriculture"

    st.subheader("Observation")
    st.write(observation)

    st.subheader("Result")
    st.write(result)

    st.subheader("Conclusion")
    st.write(conclusion)

    st.subheader("Applications")
    st.write(applications)

    data = np.random.randn(20).cumsum() + moisture
    st.area_chart(data)

    # Quiz
    st.subheader("🧠 Quiz")
    q = st.radio("Used in?",
                 ["Agriculture", "Gaming", "Networking"], key="sq")

    if st.button("Submit Quiz", key="sbtn"):
        if q == "Agriculture":
            st.success("Correct ✅")
        else:
            st.error("Wrong ❌")

    pdf = generate_pdf("Soil Moisture Sensor", aim, materials, theory,
                       procedure, observation, result, conclusion, applications)

    st.download_button("📄 Download Report", pdf, "soil.pdf")

# =======================
# HUMIDITY SENSOR
# =======================
elif lab == "Humidity Sensor":

    st.header("💧 Humidity Sensor")

    aim = "To study humidity monitoring."
    materials = "DHT11 Sensor, Microcontroller, Wires"
    theory = "Measures moisture in air."
    procedure = """1. Connect sensor
2. Read humidity
3. Display"""

    st.subheader("Aim")
    st.write(aim)

    st.subheader("Materials Required")
    st.write(materials)

    st.subheader("Theory")
    st.write(theory)

    st.subheader("Procedure")
    st.write(procedure)

    humidity = st.slider("Humidity (%)", 0, 100, 50)

    if humidity > 80:
        result = "High Humidity"
        st.warning(result)
    elif humidity < 30:
        result = "Low Humidity"
        st.warning(result)
    else:
        result = "Comfort Level"
        st.success(result)

    observation = "Humidity varies."
    conclusion = "Useful for environment monitoring."
    applications = "Weather, Homes"

    st.subheader("Observation")
    st.write(observation)

    st.subheader("Result")
    st.write(result)

    st.subheader("Conclusion")
    st.write(conclusion)

    st.subheader("Applications")
    st.write(applications)

    data = np.random.randn(20).cumsum() + humidity
    st.line_chart(data)

    # Quiz
    st.subheader("🧠 Quiz")
    q = st.radio("Measures?",
                 ["Air moisture", "Light", "Sound"], key="hq")

    if st.button("Submit Quiz", key="hbtn"):
        if q == "Air moisture":
            st.success("Correct ✅")
        else:
            st.error("Wrong ❌")

    pdf = generate_pdf("Humidity Sensor", aim, materials, theory,
                       procedure, observation, result, conclusion, applications)

    st.download_button("📄 Download Report", pdf, "humidity.pdf")
