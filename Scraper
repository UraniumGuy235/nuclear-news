# streamlit_app.py
import streamlit as st
from scraper import load_nuclear_projects, load_news_data
import pandas as pd
import json

st.set_page_config(page_title="Global Nuclear Construction Tracker", layout="wide")

st.title("\U0001F9F1 Global Nuclear Construction Tracker")

# Load data
projects = load_nuclear_projects()
news = load_news_data()

# Sidebar Filters
countries = sorted(list(set([proj['country'] for proj in projects])))
reactor_types = sorted(list(set([proj['reactor_type'] for proj in projects])))

selected_country = st.sidebar.selectbox("Filter by Country", ["All"] + countries)
selected_reactor = st.sidebar.selectbox("Filter by Reactor Type", ["All"] + reactor_types)

# Filter logic
filtered_projects = [p for p in projects if 
                     (selected_country == "All" or p['country'] == selected_country) and
                     (selected_reactor == "All" or p['reactor_type'] == selected_reactor)]

# Project Explorer
st.subheader("Project Explorer")
st.write(f"Displaying {len(filtered_projects)} projects.")
st.dataframe(pd.DataFrame(filtered_projects))

# News Section
st.subheader("Latest News")
for article in news:
    st.markdown(f"**[{article['title']}]({article['url']})**  ")
    st.markdown(f"*{article['date']} - {article['source']}*")
    st.text(article['summary'])
    st.markdown("---")
