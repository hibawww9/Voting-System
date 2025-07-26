mport streamlit as st
from PIL import Image

# ---------------- SIDEBAR ----------------
st.sidebar.header("📤 Upload Section")

# Checkbox to upload picture
upload_option = st.sidebar.checkbox("Are you willing to upload a picture?")

if upload_option:
    uploaded_image = st.sidebar.file_uploader("Upload your picture", type=["jpg", "jpeg", "png"])
    if uploaded_image:
        st.sidebar.image(uploaded_image, caption="Uploaded Picture", use_column_width=True)

# ---------------- MAIN PAGE ----------------
st.title("🗳️ VOTING USER PROFILE")
st.markdown("---")

# ----------- Input Fields ------------
name = st.text_input("Enter your full name")
number = st.text_input("Enter your phone number")
address = st.text_area("Enter your address")
age = st.slider("Enter your age", min_value=0, max_value=100)

gender = st.radio("Select your gender", options=["Male", "Female", "Other"])
nationality = st.selectbox("Select your nationality", options=["Indian", "Other"])
voter_id = st.text_input("Enter your Voter ID (if any) [Optional]")

agree = st.checkbox("I confirm that the above information is correct.")

submit = st.button("Submit")

# ---------- Display Section ----------
if submit:
    if not (name and number and address and agree):
        st.warning("⚠️ Please complete all required fields and agree to the terms.")
    else:
        st.success("✅ Profile submitted successfully!")
        
        st.subheader("📄 Your Details:")
        col1, col2 = st.columns(2)
        with col1:
            st.write(f"**Name:** {name}")
            st.write(f"**Phone Number:** {number}")
            st.write(f"**Gender:** {gender}")
            st.write(f"**Nationality:** {nationality}")
        with col2:
            st.write(f"**Age:** {age}")
            st.write(f"**Address:** {address}")
            st.write(f"**Voter ID:** {voter_id if voter_id else 'Not provided'}")

        # Eligibility Logic
        if age > 18 and nationality == "Indian":
            st.markdown("<div style='color:green; font-weight:bold;'>🎉 You are eligible to vote in India!</div>", unsafe_allow_html=True)
        elif nationality != "Indian":
            st.markdown("<div style='color:red; font-weight:bold;'>❌ Only Indian citizens are eligible to vote in India.</div>", unsafe_allow_html=True)
        else:
            st.markdown("<div style='color:red; font-weight:bold;'>⚠️ You must be over 18 years old to be eligible to vote.</div>", unsafe_allow_html=True)
