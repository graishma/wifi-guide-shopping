# app.py
import streamlit as st
import json
import os
import urllib.parse
import base64

# ---------- background and styling ----------
BG_FILE = "wifi img.jpg"
if os.path.exists(BG_FILE):
    with open(BG_FILE, "rb") as f:
        b64 = base64.b64encode(f.read()).decode()
    st.markdown(f"""
    <style>
    .stApp {{
        background-image: url("data:image/jpg;base64,{b64}");
        background-size: cover;
        background-position: center;
        background-attachment: fixed;
        z-index: 0;
        
    }}
    .stApp::before {{
        content: "";
        position: fixed;
        top:0; left:0; width:100%; height:100%;
        background: rgba(255,255,255,0.6);
        z-index: -1;
    }}
    .stMarkdown, .stText, .stHeader, .stSubheader, .stTitle, .stRadio label {{
        color: #111111 !important;
        text-shadow: 0px 0px 6px rgba(0,0,0,0.7);
    }}
    button {{
        background-color: #2563eb;
        color: white;
        border: none;
        padding: 6px 10px;
        border-radius: 6px;
        cursor: pointer;
    }}
    button:hover {{
        background-color: #1e40af;
    }}
    </style>
    """, unsafe_allow_html=True)
else:
    st.warning(f"Background '{BG_FILE}' not found. Place it next to app.py.")

def amazon_search_link(name: str) -> str:
    q = urllib.parse.quote_plus(name + " router")
    return f"https://www.amazon.in/s?k={q}"
def flipkart_search_link(name: str) -> str:
    q = urllib.parse.quote_plus(name + " router")
    return f"https://www.flipkart.com/search?q={q}"
def store_button(url: str, label: str):
    st.markdown(f'<a href="{url}" target="_blank"><button>{label}</button></a>', unsafe_allow_html=True)

# ---------- products (100 routers) ----------
products = [
    {"name":"TP-Link Archer AX11000",
     "description":"Tri-band Wi-Fi 6 gaming router.\nDelivers speeds up to 10.8 Gbps.\nOptimized for 4K streaming and online gaming.",
     "amazon": amazon_search_link("TP-Link Archer AX11000"),
     "flipkart": flipkart_search_link("TP-Link Archer AX11000")},
    {"name":"Netgear Nighthawk AX8 (RAX80)",
     "description":"8-stream Wi-Fi 6 router for ultra-low latency.\nGreat for gaming and VR.\nSupports MU-MIMO and QoS.",
     "amazon": amazon_search_link("Netgear Nighthawk RAX80 AX8"),
     "flipkart": flipkart_search_link("Netgear Nighthawk RAX80")},
    {"name":"Asus RT-AX88U",
     "description":"High-performance Wi-Fi 6 with 8 LAN ports.\nAiMesh support for whole-home coverage.\nExcellent for power users and streamers.",
     "amazon": amazon_search_link("Asus RT-AX88U"),
     "flipkart": flipkart_search_link("Asus RT-AX88U")},
    {"name":"D-Link DIR-825",
     "description":"Dual-band AC1200 router with parental controls.\nGuest Wi-Fi and good basic performance.\nAffordable for small homes.",
     "amazon": amazon_search_link("D-Link DIR-825"),
     "flipkart": flipkart_search_link("D-Link DIR-825")},
    {"name":"Linksys MR8300",
     "description":"Tri-band mesh-ready router.\nVelop-compatible for easy mesh expansion.\nGood for smart-home setups.",
     "amazon": amazon_search_link("Linksys MR8300"),
     "flipkart": flipkart_search_link("Linksys MR8300")},
    {"name":"Xiaomi Mi Router 4A",
     "description":"Budget dual-band router with 4 antennas.\nApp-managed setup and controls.\nGreat value for small apartments.",
     "amazon": amazon_search_link("Xiaomi Mi Router 4A"),
     "flipkart": flipkart_search_link("Xiaomi Mi Router 4A")},
    {"name":"TP-Link Archer AX6000",
     "description":"Wi-Fi 6 router with 8 Gigabit LAN ports.\nPowerful CPU for heavy throughput.\nExcellent for large households & streaming.",
     "amazon": amazon_search_link("TP-Link Archer AX6000"),
     "flipkart": flipkart_search_link("TP-Link Archer AX6000")},
    {"name":"Netgear Orbi RBK752",
     "description":"Wi-Fi 6 mesh system (2-pack) for large homes.\nSeamless roaming and strong backhaul.\nGreat for dense device environments.",
     "amazon": amazon_search_link("Netgear Orbi RBK752"),
     "flipkart": flipkart_search_link("Netgear Orbi RBK752")},
    {"name":"Asus ROG Rapture GT-AX11000",
     "description":"Tri-band gaming router with low-latency features.\nMultiple gaming-specific QoS and ports.\nHigh-end gaming performance.",
     "amazon": amazon_search_link("Asus ROG Rapture GT-AX11000"),
     "flipkart": flipkart_search_link("Asus ROG Rapture GT-AX11000")},
    {"name":"D-Link DIR-615",
     "description":"Affordable N300 router for basic internet use.\nEasy setup for non-technical users.\nSuitable for small homes or backups.",
     "amazon": amazon_search_link("D-Link DIR-615"),
     "flipkart": flipkart_search_link("D-Link DIR-615")},
    {"name":"Linksys EA7500",
     "description":"AC1900 dual-band router with MU-MIMO.\nGood for multiple HD streams and gaming.\nSimple management and reliable performance.",
     "amazon": amazon_search_link("Linksys EA7500"),
     "flipkart": flipkart_search_link("Linksys EA7500")},
    {"name":"Tenda AC10",
     "description":"Budget AC1200 router with 4 antennas.\nDecent wireless coverage for homes.\nSimple mobile app control.",
     "amazon": amazon_search_link("Tenda AC10"),
     "flipkart": flipkart_search_link("Tenda AC10")},
    {"name":"TP-Link Deco M9 Plus",
     "description":"Tri-band mesh Wi-Fi with integrated smart hub.\nWhole-home coverage and IoT integration.\nGood for smart-home ecosystems.",
     "amazon": amazon_search_link("TP-Link Deco M9 Plus"),
     "flipkart": flipkart_search_link("TP-Link Deco M9 Plus")},
    {"name":"Netgear Orbi RBK50",
     "description":"Popular dual-band Orbi mesh (2-pack).\nStrong coverage and easy setup.\nGood for larger homes with many clients.",
     "amazon": amazon_search_link("Netgear Orbi RBK50"),
     "flipkart": flipkart_search_link("Netgear Orbi RBK50")},
    {"name":"Asus RT-AC86U",
     "description":"AC2900 dual-band router tuned for gaming.\nAdaptive QoS and AiProtection.\nStrong mid-high tier performance.",
     "amazon": amazon_search_link("Asus RT-AC86U"),
     "flipkart": flipkart_search_link("Asus RT-AC86U")},
    {"name":"D-Link DIR-882",
     "description":"AC2600 router with MU-MIMO support.\nGood for HD streaming and gaming.\nStable and reliable in medium homes.",
     "amazon": amazon_search_link("D-Link DIR-882"),
     "flipkart": flipkart_search_link("D-Link DIR-882")},
    {"name":"Linksys EA9500",
     "description":"AC5400 tri-band router for many devices.\nHigh throughput and USB sharing.\nSuitable for power users and NAS setups.",
     "amazon": amazon_search_link("Linksys EA9500"),
     "flipkart": flipkart_search_link("Linksys EA9500")},
    {"name":"Tenda AC15",
     "description":"AC1900 dual-band router at budget price.\nGood streaming capability and range.\nEasy mobile management.",
     "amazon": amazon_search_link("Tenda AC15"),
     "flipkart": flipkart_search_link("Tenda AC15")},
    {"name":"TP-Link Deco X60",
     "description":"Wi-Fi 6 mesh kit for whole-home coverage.\nAX performance across nodes.\nSimple app control & parental controls.",
     "amazon": amazon_search_link("TP-Link Deco X60"),
     "flipkart": flipkart_search_link("TP-Link Deco X60")},
    {"name":"Netgear Nighthawk R7000",
     "description":"AC1900 classic Nighthawk router.\nGood firmware support and features.\nSolid performance for small-medium homes.",
     "amazon": amazon_search_link("Netgear Nighthawk R7000"),
     "flipkart": flipkart_search_link("Netgear Nighthawk R7000")},
    {"name":"Asus RT-AC68U",
     "description":"AC1900 router with AiProtection and USB 3.0.\nStrong overall performance for home users.\nSupports AiMesh for expansion.",
     "amazon": amazon_search_link("Asus RT-AC68U"),
     "flipkart": flipkart_search_link("Asus RT-AC68U")},
    {"name":"TP-Link Archer C7",
     "description":"AC1750 dual-band router offering balance of value and speed.\nGood for 4K streaming and gaming.\nWide compatibility and easy setup.",
     "amazon": amazon_search_link("TP-Link Archer C7"),
     "flipkart": flipkart_search_link("TP-Link Archer C7")},
    {"name":"Netgear Orbi RBK852",
     "description":"High-end Wi-Fi 6 mesh system for very large homes.\nExceptional throughput and range.\nGreat for many simultaneous devices.",
     "amazon": amazon_search_link("Netgear Orbi RBK852"),
     "flipkart": flipkart_search_link("Netgear Orbi RBK852")},
    {"name":"Linksys Velop MX4200",
     "description":"Tri-band Wi-Fi 6 mesh for multi-device homes.\nEasy setup and stable roaming.\nGood for smart home networks.",
     "amazon": amazon_search_link("Linksys Velop MX4200"),
     "flipkart": flipkart_search_link("Linksys Velop MX4200")},
    {"name":"TP-Link Archer AX73",
     "description":"AX5400 Wi-Fi 6 router with strong range.\nGood throughput for 1 Gbps plans.\nGreat mid-high tier everyday router.",
     "amazon": amazon_search_link("TP-Link Archer AX73"),
     "flipkart": flipkart_search_link("TP-Link Archer AX73")},
    {"name":"Asus RT-AX58U",
     "description":"AX3000 Wi-Fi 6 router with AiMesh support.\nStrong performance for streaming and gaming.\nCompact form factor.",
     "amazon": amazon_search_link("Asus RT-AX58U"),
     "flipkart": flipkart_search_link("Asus RT-AX58U")},
    {"name":"D-Link COVR-C1203",
     "description":"AC1200 mesh kit for whole-home coverage.\nEasy to expand and manage.\nGood value mesh solution.",
     "amazon": amazon_search_link("D-Link COVR-C1203"),
     "flipkart": flipkart_search_link("D-Link COVR-C1203")},
    {"name":"Netgear RAX50",
     "description":"AX5400 Wi-Fi 6 router with fast throughput.\nOptimized for streaming and many devices.\nGood performance/price balance.",
     "amazon": amazon_search_link("Netgear RAX50"),
     "flipkart": flipkart_search_link("Netgear RAX50")},
    {"name":"Linksys EA8100",
     "description":"AC2600 dual-band router for streaming.\nReliable performance with MU-MIMO.\nGood USB and LAN options.",
     "amazon": amazon_search_link("Linksys EA8100"),
     "flipkart": flipkart_search_link("Linksys EA8100")},
    {"name":"Tenda AC8",
     "description":"Compact AC1200 router with MU-MIMO.\nAffordable, easy to manage via app.\nGood for apartments and small homes.",
     "amazon": amazon_search_link("Tenda AC8"),
     "flipkart": flipkart_search_link("Tenda AC8")},
    {"name":"TP-Link Archer AX20",
     "description":"AX1800 Wi-Fi 6 dual-band router.\nGreat budget-friendly AX performance.\nEasy management through app.",
     "amazon": amazon_search_link("TP-Link Archer AX20"),
     "flipkart": flipkart_search_link("TP-Link Archer AX20")},
    {"name":"Xiaomi AX3600",
     "description":"AX3000/AX3600 style router with many antennas.\nGood performance for the price.\nSuited to fast fiber connections.",
     "amazon": amazon_search_link("Xiaomi AX3600 router"),
     "flipkart": flipkart_search_link("Xiaomi AX3600")},
    {"name":"Netgear Nighthawk XR500",
     "description":"Gaming router with low-latency Geo-Filter.\nCustomizable dashboard for gamers.\nOptimized routing for games.",
     "amazon": amazon_search_link("Netgear Nighthawk XR500"),
     "flipkart": flipkart_search_link("Netgear Nighthawk XR500")},
    {"name":"Asus RT-AX86U",
     "description":"AX5700 gaming router with 2.5G port.\nExcellent latency control and QoS.\nStrong all-around performer.",
     "amazon": amazon_search_link("Asus RT-AX86U"),
     "flipkart": flipkart_search_link("Asus RT-AX86U")},
    {"name":"D-Link R15 Eagle Pro AI",
     "description":"AI-optimized router with AX1500 specs.\nSimplified setup and optimization.\nGood for casual streaming/gaming.",
     "amazon": amazon_search_link("D-Link R15 Eagle Pro AI"),
     "flipkart": flipkart_search_link("D-Link R15 Eagle Pro AI")},
    {"name":"TP-Link Archer A7",
     "description":"AC1750 dual-band router with Alexa support.\nReliable and widely used model.\nGood balance of features & price.",
     "amazon": amazon_search_link("TP-Link Archer A7"),
     "flipkart": flipkart_search_link("TP-Link Archer A7")},
    {"name":"Linksys WRT3200ACM",
     "description":"Open-source friendly router with strong hardware.\nTri-stream and advanced features.\nFavored by tinkerers and prosumers.",
     "amazon": amazon_search_link("Linksys WRT3200ACM"),
     "flipkart": flipkart_search_link("Linksys WRT3200ACM")},
    {"name":"Tenda Nova MW6",
     "description":"AC1200 mesh pack for easy coverage.\nAffordable mesh solution for medium homes.\nSimple app and parental controls.",
     "amazon": amazon_search_link("Tenda Nova MW6"),
     "flipkart": flipkart_search_link("Tenda Nova MW6")},
    {"name":"TP-Link Archer C1200",
     "description":"AC1200 router with stable performance.\nGood for streaming and remote work.\nBudget-friendly choice.",
     "amazon": amazon_search_link("TP-Link Archer C1200"),
     "flipkart": flipkart_search_link("TP-Link Archer C1200")},
    {"name":"Netgear Orbi RBK963",
     "description":"High-end Orbi Wi-Fi 6 mesh (tri-band premium).\nMassive coverage and throughput.\nDesigned for heavy multi-user homes.",
     "amazon": amazon_search_link("Netgear Orbi RBK963"),
     "flipkart": flipkart_search_link("Netgear Orbi RBK963")},
    {"name":"Asus ZenWiFi XT8",
     "description":"AX6600 tri-band mesh system.\nExcellent coverage and features.\nGreat for large homes and many devices.",
     "amazon": amazon_search_link("Asus ZenWiFi XT8"),
     "flipkart": flipkart_search_link("Asus ZenWiFi XT8")},
    {"name":"D-Link EXO AX5400",
     "description":"AX5400 router with good coverage.\nAI features to optimize performance.\nGreat mid-high tier router.",
     "amazon": amazon_search_link("D-Link EXO AX5400"),
     "flipkart": flipkart_search_link("D-Link EXO AX5400")},
    {"name":"Linksys MX5300 (Velop)",
     "description":"Mesh kit with Wi-Fi 6 performance.\nEasy expansion and stable coverage.\nGood for busy smart homes.",
     "amazon": amazon_search_link("Linksys MX5300 Velop"),
     "flipkart": flipkart_search_link("Linksys MX5300 Velop")},
    {"name":"TP-Link Archer AX50",
     "description":"AX3000 dual-band with Intel chipset.\nStrong mid-range AX performance.\nGood for streaming and gaming.",
     "amazon": amazon_search_link("TP-Link Archer AX50"),
     "flipkart": flipkart_search_link("TP-Link Archer AX50")},
    {"name":"Asus ROG GT-AXE11000",
     "description":"Wi-Fi 6E gaming flagship with tri-band.\nOptimized for ultra-low latency.\nPacked with gaming features and ports.",
     "amazon": amazon_search_link("Asus ROG GT-AXE11000"),
     "flipkart": flipkart_search_link("Asus ROG GT-AXE11000")},
    {"name":"Netgear Nighthawk RAX200",
     "description":"Tri-band AX11000-class performance.\nExcellent for very high throughput needs.\nFeature-rich for advanced users.",
     "amazon": amazon_search_link("Netgear RAX200"),
     "flipkart": flipkart_search_link("Netgear RAX200")},
    {"name":"TP-Link Archer AX10",
     "description":"Entry-level AX1500 Wi-Fi 6 router.\nGreat for basic fiber plans.\nBudget-friendly modern features.",
     "amazon": amazon_search_link("TP-Link Archer AX10"),
     "flipkart": flipkart_search_link("TP-Link Archer AX10")},
    {"name":"Xiaomi Redmi AX5",
     "description":"Affordable AX1800 Wi-Fi 6 router.\nGood range and app controls.\nExcellent value for money.",
     "amazon": amazon_search_link("Redmi AX5 router"),
     "flipkart": flipkart_search_link("Redmi AX5")},
    {"name":"Mercusys MR70X",
     "description":"AX1800 budget Wi-Fi 6 router.\nSimple setup, decent range for small homes.\nGreat price-to-performance ratio.",
     "amazon": amazon_search_link("Mercusys MR70X"),
     "flipkart": flipkart_search_link("Mercusys MR70X")},
    {"name":"Cudy AC1200",
     "description":"Affordable AC1200 router with stable throughput.\nSuitable for small to medium homes.\nEasy management via web UI.",
     "amazon": amazon_search_link("Cudy AC1200 router"),
     "flipkart": flipkart_search_link("Cudy AC1200")},
    {"name":"TOTOLINK A3000RU",
     "description":"AC1200 gigabit router with reliable performance.\nGood for streaming and multiple clients.\nBudget-oriented hardware.",
     "amazon": amazon_search_link("TOTOLINK A3000RU"),
     "flipkart": flipkart_search_link("TOTOLINK A3000RU")},
    {"name":"Synology RT2600ac",
     "description":"AC2600 router with Synology Router OS.\nExcellent control, VPN, and NAS features.\nGreat for power users and small offices.",
     "amazon": amazon_search_link("Synology RT2600ac"),
     "flipkart": flipkart_search_link("Synology RT2600ac")},
    {"name":"Ubiquiti AmpliFi Alien",
     "description":"High-end mesh router with sleek design.\nPowerful performance and easy app setup.\nGreat for prosumers and smart homes.",
     "amazon": amazon_search_link("Ubiquiti AmpliFi Alien"),
     "flipkart": flipkart_search_link("Ubiquiti AmpliFi Alien")},
    {"name":"Google Nest Wifi Pro",
     "description":"Wi-Fi 6E mesh system with simple UX.\nIntegrated smart home features.\nEasy setup and management.",
     "amazon": amazon_search_link("Google Nest Wifi Pro"),
     "flipkart": flipkart_search_link("Google Nest Wifi Pro")},
    {"name":"Amazon eero Pro 6E",
     "description":"Wi-Fi 6E mesh with easy expandability.\nGood for smart-home integration.\nSimple cloud-managed experience.",
     "amazon": amazon_search_link("eero Pro 6E"),
     "flipkart": flipkart_search_link("eero Pro 6E")},
    {"name":"Reyee RG-AX1800",
     "description":"AX1800 affordable router with steady performance.\nGood entry-level AX option.\nReady for modern broadband.",
     "amazon": amazon_search_link("Reyee RG-AX1800"),
     "flipkart": flipkart_search_link("Reyee RG-AX1800")},
    {"name":"Redmi AX9000",
     "description":"High-end tri-band gaming router from Xiaomi.\nPowerful hardware for gaming & streaming.\nCompetitive pricing for features.",
     "amazon": amazon_search_link("Redmi AX9000"),
     "flipkart": flipkart_search_link("Redmi AX9000")},
    {"name":"TP-Link Archer AX73 Pro",
     "description":"Enhanced AX73 with improved throughput.\nGreat mid-high tier performance.\nGood for households with many devices.",
     "amazon": amazon_search_link("TP-Link Archer AX73 Pro"),
     "flipkart": flipkart_search_link("TP-Link Archer AX73 Pro")},
    {"name":"ASUS ZenWiFi Pro ET12",
     "description":"Top-tier Wi-Fi 6E mesh system.\nMassive coverage and future-proof tech.\nDesigned for power users and large homes.",
     "amazon": amazon_search_link("ASUS ZenWiFi Pro ET12"),
     "flipkart": flipkart_search_link("ASUS ZenWiFi Pro ET12")},
    {"name":"NETGEAR Orbi 960 (RBKE963)",
     "description":"Premium Wi-Fi 6E mesh solution.\nUltra-high throughput for many devices.\nIdeal for demanding home networks.",
     "amazon": amazon_search_link("NETGEAR Orbi 960 RBKE963"),
     "flipkart": flipkart_search_link("NETGEAR Orbi 960 RBKE963")},
    {"name":"TP-Link Deco BE85",
     "description":"Wi-Fi 7 mesh system for future-proofing.\nHigh speeds and low latency.\nGreat for large smart homes (Wi-Fi 7 ready).",
     "amazon": amazon_search_link("TP-Link Deco BE85"),
     "flipkart": flipkart_search_link("TP-Link Deco BE85")},
    {"name":"ASUS ROG Rapture GT-BE98",
     "description":"Wi-Fi 7 gaming flagship with ultra low latency.\nPacked with gaming optimizations and ports.\nTop-tier performance for competitive gamers.",
     "amazon": amazon_search_link("ASUS ROG GT-BE98"),
     "flipkart": flipkart_search_link("ASUS ROG GT-BE98")},
    {"name":"TP-Link Archer C64",
     "description":"AC1200 dual-band with stable home performance.\nEasy setup and decent range.\nBudget friendly for routine use.",
     "amazon": amazon_search_link("TP-Link Archer C64"),
     "flipkart": flipkart_search_link("TP-Link Archer C64")},
    {"name":"Mercusys Halo S12",
     "description":"AC2100 mesh kit for affordable coverage.\nSimple app-based control.\nGood for typical family homes.",
     "amazon": amazon_search_link("Mercusys Halo S12"),
     "flipkart": flipkart_search_link("Mercusys Halo S12")},
    {"name":"D-Link DIR-3060",
     "description":"Tri-band router with MU-MIMO and smart features.\nGood for streaming and multi-device homes.\nAdvanced QoS and security options.",
     "amazon": amazon_search_link("D-Link DIR-3060"),
     "flipkart": flipkart_search_link("D-Link DIR-3060")},
    {"name":"ASUS RT-AX92U",
     "description":"Tri-band mesh-ready AX router.\nGreat for AiMesh whole-home setups.\nBalanced performance and features.",
     "amazon": amazon_search_link("ASUS RT-AX92U"),
     "flipkart": flipkart_search_link("ASUS RT-AX92U")},
    {"name":"Netgear Nighthawk RAXE300",
     "description":"Wi-Fi 6E compact router with solid performance.\nGood for home offices and gaming.\nFuture friendly with 6GHz support.",
     "amazon": amazon_search_link("Netgear RAXE300"),
     "flipkart": flipkart_search_link("Netgear RAXE300")},
    {"name":"Linksys Hydra Pro 6",
     "description":"AX5400 Wi-Fi 6 router with mesh capabilities.\nGood multi-device handling and range.\nDesigned for modern smart homes.",
     "amazon": amazon_search_link("Linksys Hydra Pro 6"),
     "flipkart": flipkart_search_link("Linksys Hydra Pro 6")},
    {"name":"TP-Link Archer AX21",
     "description":"AX1800 entry-level Wi-Fi 6 router.\nGreat price-to-performance for new AX users.\nStable and easy to manage.",
     "amazon": amazon_search_link("TP-Link Archer AX21"),
     "flipkart": flipkart_search_link("TP-Link Archer AX21")},
    {"name":"ASUS TUF-AX5400",
     "description":"Gaming-tuned AX5400 router with durable design.\nGood value for gamers and streamers.\nRobust QoS and security features.",
     "amazon": amazon_search_link("ASUS TUF-AX5400"),
     "flipkart": flipkart_search_link("ASUS TUF-AX5400")},
    {"name":"Netgear Nighthawk RAXE500",
     "description":"High-end Wi-Fi 6E router for extreme throughput.\nExcellent for many high-demand clients.\n6GHz band for future use.",
     "amazon": amazon_search_link("Netgear RAXE500"),
     "flipkart": flipkart_search_link("Netgear RAXE500")},
    {"name":"TP-Link Archer C20",
     "description":"Basic AC750/AC1200 model for simple needs.\nCompact and inexpensive.\nGood for small apartments.",
     "amazon": amazon_search_link("TP-Link Archer C20"),
     "flipkart": flipkart_search_link("TP-Link Archer C20")},
    {"name":"D-Link DIR-867",
     "description":"AC1750 with solid mid-range performance.\nGood value for streaming and gaming.\nEasy setup and stable firmware.",
     "amazon": amazon_search_link("D-Link DIR-867"),
     "flipkart": flipkart_search_link("D-Link DIR-867")},
    {"name":"Xiaomi Mesh System AX3000",
     "description":"AX3000 mesh kit for consistent coverage.\nGood price/perf for modern homes.\nApp-controlled and easy to deploy.",
     "amazon": amazon_search_link("Xiaomi Mesh System AX3000"),
     "flipkart": flipkart_search_link("Xiaomi Mesh System AX3000")},
    {"name":"Linksys EA6400",
     "description":"Value AC router with simple controls.\nDecent throughput for small homes.\nGood legacy device compatibility.",
     "amazon": amazon_search_link("Linksys EA6400"),
     "flipkart": flipkart_search_link("Linksys EA6400")},
    {"name":"TP-Link Archer AX73 (alt)",
     "description":"AX5400 strong-range router with stable throughput.\nGreat for households with multiple devices.\nFeature-rich and user-friendly app.",
     "amazon": amazon_search_link("TP-Link Archer AX73"),
     "flipkart": flipkart_search_link("TP-Link Archer AX73")},
    {"name":"Netgear Orbi RBK23",
     "description":"Dual-band mesh kit for medium homes.\nSimple UI and easy expansion.\nReliable coverage across living spaces.",
     "amazon": amazon_search_link("Netgear Orbi RBK23"),
     "flipkart": flipkart_search_link("Netgear Orbi RBK23")},
    {"name":"ASUS Lyra Trio",
     "description":"AC1750 mesh kit focused on stable coverage.\nPlug-and-play with decent speeds.\nGood for non-technical users.",
     "amazon": amazon_search_link("ASUS Lyra Trio"),
     "flipkart": flipkart_search_link("ASUS Lyra Trio")},
    {"name":"D-Link DIR-601",
     "description":"Legacy N300 router for basic tasks.\nVery low-cost and compact.\nGood for simple home internet use.",
     "amazon": amazon_search_link("D-Link DIR-601"),
     "flipkart": flipkart_search_link("D-Link DIR-601")},
    {"name":"TP-Link Archer C9",
     "description":"AC1900 router with USB sharing.\nGood balance of range and speed.\nSolid mid-range performer.",
     "amazon": amazon_search_link("TP-Link Archer C9"),
     "flipkart": flipkart_search_link("TP-Link Archer C9")},
    {"name":"Netgear Nighthawk RAX43",
     "description":"AX & modern mid-tier performance for home use.\nGood for streaming and remote work.\nCompact and featureful.",
     "amazon": amazon_search_link("Netgear Nighthawk RAX43"),
     "flipkart": flipkart_search_link("Netgear Nighthawk RAX43")},
    {"name":"Linksys EA7300",
     "description":"AC1750 router offering smooth streaming.\nMU-MIMO support and stable throughput.\nGood value for multi-device households.",
     "amazon": amazon_search_link("Linksys EA7300"),
     "flipkart": flipkart_search_link("Linksys EA7300")},
    {"name":"Tenda AC5",
     "description":"Budget AC1200 router with decent range.\nSimple to install and manage.\nExcellent price-per-performance.",
     "amazon": amazon_search_link("Tenda AC5"),
     "flipkart": flipkart_search_link("Tenda AC5")},
    {"name":"TP-Link Archer AX90",
     "description":"Tri-band AX6600 router with high throughput.\nGreat for mixed heavy usage scenarios.\nPowerful CPU and many features.",
     "amazon": amazon_search_link("TP-Link Archer AX90"),
     "flipkart": flipkart_search_link("TP-Link Archer AX90")},
    {"name":"ASUS RT-AXE7800",
     "description":"Wi-Fi 6E capable router with wide compatibility.\nExtra 6GHz band for future devices.\nHigh throughput for demanding households.",
     "amazon": amazon_search_link("ASUS RT-AXE7800"),
     "flipkart": flipkart_search_link("ASUS RT-AXE7800")},
    {"name":"NETGEAR Orbi RBK852 (alt)",
     "description":"Premium mesh for large houses and many devices.\nExcellent throughput and easy app control.\nHighly rated for reliability.",
     "amazon": amazon_search_link("Netgear Orbi RBK852"),
     "flipkart": flipkart_search_link("Netgear Orbi RBK852")},
    {"name":"TP-Link Archer AX73 Dual",
     "description":"Variant of AX73 with solid specs.\nGood family-friendly performance.\nStrong software and parental controls.",
     "amazon": amazon_search_link("TP-Link Archer AX73 Dual"),
     "flipkart": flipkart_search_link("TP-Link Archer AX73 Dual")},
    {"name":"Xiaomi Router AX9000 (gaming)",
     "description":"High-performance tri-band gaming router.\nMultiple wired ports and QoS.\nGreat for competitive gaming households.",
     "amazon": amazon_search_link("Xiaomi AX9000 router"),
     "flipkart": flipkart_search_link("Xiaomi AX9000")},
    {"name":"Linksys Velop AC1300",
     "description":"Affordable mesh kit for basic whole-home coverage.\nSimple setup and app control.\nGood for small-to-medium homes.",
     "amazon": amazon_search_link("Linksys Velop AC1300"),
     "flipkart": flipkart_search_link("Linksys Velop AC1300")},
    {"name":"D-Link EXO AC3000",
     "description":"Tri-band AC3000 with smart features.\nGood for streaming and multiple clients.\nBalanced performance and options.",
     "amazon": amazon_search_link("D-Link EXO AC3000"),
     "flipkart": flipkart_search_link("D-Link EXO AC3000")},
    {"name":"TP-Link Archer AXE75 (Wi-Fi 6E)",
     "description":"Wi-Fi 6E router with 6GHz support.\nGreat for future devices and low-latency apps.\nHigh performance for streaming & gaming.",
     "amazon": amazon_search_link("TP-Link Archer AXE75"),
     "flipkart": flipkart_search_link("TP-Link Archer AXE75")},
    {"name":"ASUS RT-AC3200",
     "description":"Tri-band AC3200 router for multi-device homes.\nGood for streaming and medium gaming.\nSturdy build and solid features.",
     "amazon": amazon_search_link("ASUS RT-AC3200"),
     "flipkart": flipkart_search_link("ASUS RT-AC3200")},
    {"name":"Netgear Nighthawk Pro Gaming XR700",
     "description":"High-end gaming router with specialized features.\nAdvanced controls for latency and routing.\nBuilt for competitive setups.",
     "amazon": amazon_search_link("Netgear Nighthawk Pro Gaming XR700"),
     "flipkart": flipkart_search_link("Netgear Nighthawk Pro Gaming XR700")},
    {"name":"TP-Link Deco M4",
     "description":"Affordable mesh system for home coverage.\nEasy to deploy and manage via app.\nGreat value for multi-room coverage.",
     "amazon": amazon_search_link("TP-Link Deco M4"),
     "flipkart": flipkart_search_link("TP-Link Deco M4")},
    {"name":"Synology RT6600ax",
     "description":"High-end router with advanced NAS-like features.\nExcellent for SMB and power users.\nStrong security and VPN options.",
     "amazon": amazon_search_link("Synology RT6600ax"),
     "flipkart": flipkart_search_link("Synology RT6600ax")},
    {"name":"Ubiquiti UniFi Dream Router",
     "description":"All-in-one UniFi router and controller.\nGreat for prosumers and small offices.\nPowerful networking features and VPN.",
     "amazon": amazon_search_link("Ubiquiti UniFi Dream Router"),
     "flipkart": flipkart_search_link("Ubiquiti UniFi Dream Router")},
    {"name":"TP-Link Archer AX12",
     "description":"AX1500/AX1800 level entry AX device.\nGood price-to-performance for small homes.\nEasy to manage with the Tether app.",
     "amazon": amazon_search_link("TP-Link Archer AX12"),
     "flipkart": flipkart_search_link("TP-Link Archer AX12")},
    {"name":"NETGEAR Orbi RBK50S",
     "description":"Updated Orbi design with easier management.\nStable mesh coverage across household.\nGood for many connected devices.",
     "amazon": amazon_search_link("NETGEAR Orbi RBK50S"),
     "flipkart": flipkart_search_link("NETGEAR Orbi RBK50S")},
    {"name":"ASUS ZenWiFi XD4",
     "description":"AX1800 mesh kit for easy whole-home coverage.\nGood balance of speed and price.\nFriendly app and parental controls.",
     "amazon": amazon_search_link("ASUS ZenWiFi XD4"),
     "flipkart": flipkart_search_link("ASUS ZenWiFi XD4")},
    {"name":"Redmi Router AC2100",
     "description":"Affordable AC2100 for everyday streaming.\nDecent feature set and app support.\nGreat value for price-conscious buyers.",
     "amazon": amazon_search_link("Redmi Router AC2100"),
     "flipkart": flipkart_search_link("Redmi Router AC2100")},
    {"name":"Mercusys MR50G",
     "description":"Affordable AX3000-class router for budget buyers.\nStrong basic AX performance.\nEasy setup with mobile app.",
     "amazon": amazon_search_link("Mercusys MR50G"),
     "flipkart": flipkart_search_link("Mercusys MR50G")},
    {"name":"NETGEAR Orbi RBK13",
     "description":"Compact mesh kit for small homes.\nSimple and affordable mesh solution.\nGood consumer-focused UX.",
     "amazon": amazon_search_link("NETGEAR Orbi RBK13"),
     "flipkart": flipkart_search_link("NETGEAR Orbi RBK13")},
    {"name":"TP-Link Archer AX90 Pro",
     "description":"Updated AX90 variant with improved CPU.\nHigh throughput for heavy households.\nGreat mix of features and performance.",
     "amazon": amazon_search_link("TP-Link Archer AX90 Pro"),
     "flipkart": flipkart_search_link("TP-Link Archer AX90 Pro")},
    {"name":"ASUS ROG Rapture GT-AC2900",
     "description":"AC2900 gaming router with robust QoS.\nDesigned for competitive gamers.\nGood features for streaming & voice chat.",
     "amazon": amazon_search_link("ASUS ROG Rapture GT-AC2900"),
     "flipkart": flipkart_search_link("ASUS ROG Rapture GT-AC2900")},
    {"name":"D-Link EXO DIR-3060",
     "description":"Tri-band EXO router with AI features.\nGood for heavy media streaming.\nBalanced features and administration.",
     "amazon": amazon_search_link("D-Link EXO DIR-3060"),
     "flipkart": flipkart_search_link("D-Link EXO DIR-3060")},
    {"name":"TP-Link Archer AXE75 (6E)",
     "description":"Wi-Fi 6E capable router with 6GHz band.\nFuture-proof with strong throughput.\nGreat for gaming and low-latency apps.",
     "amazon": amazon_search_link("TP-Link Archer AXE75"),
     "flipkart": flipkart_search_link("TP-Link Archer AXE75")},
    {"name":"Netgear N300 (WNR2020)",
     "description":"Very basic N300 router for simple tasks.\nUltra-budget, compact and easy to setup.\nWorks well as a secondary AP.",
     "amazon": amazon_search_link("Netgear WNR2020 N300"),
     "flipkart": flipkart_search_link("Netgear WNR2020")},
    {"name":"Linksys EA8300",
     "description":"AC2200 tri-band capable router.\nGood mid-tier performance and features.\nSimple admin and stable firmware.",
     "amazon": amazon_search_link("Linksys EA8300"),
     "flipkart": flipkart_search_link("Linksys EA8300")},
    {"name":"Tenda AC23",
     "description":"AC2100 budget performer with multiple antennas.\nDesigned for home streaming and gaming.\nGood wireless coverage.",
     "amazon": amazon_search_link("Tenda AC23"),
     "flipkart": flipkart_search_link("Tenda AC23")},
    {"name":"ASUS RT-AX3000",
     "description":"AX3000 dual-band with strong fundamentals.\nGreat for modern households and streaming.\nGood software feature set.",
     "amazon": amazon_search_link("ASUS RT-AX3000"),
     "flipkart": flipkart_search_link("ASUS RT-AX3000")},
    {"name":"TP-Link Deco S4",
     "description":"Affordable AC1200 mesh kit for whole-home coverage.\nSimple setup and maintenance.\nGood value-based mesh option.",
     "amazon": amazon_search_link("TP-Link Deco S4"),
     "flipkart": flipkart_search_link("TP-Link Deco S4")},
    {"name":"Netgear Nighthawk RAX43",
     "description":"Compact AX router with solid mid-range performance.\nDesigned for streaming & home offices.\nBalanced features and sizing.",
     "amazon": amazon_search_link("Netgear RAX43"),
     "flipkart": flipkart_search_link("Netgear RAX43")},
    {"name":"Linksys Velop MX10600",
     "description":"High-end Velop mesh with Wi-Fi 6E support.\nExcellent coverage and device handling.\nPremium hardware and UX.",
     "amazon": amazon_search_link("Linksys Velop MX10600"),
     "flipkart": flipkart_search_link("Linksys Velop MX10600")},
    {"name":"TP-Link Archer C5",
     "description":"AC1200 small home router with decent range.\nGood price-performance for basic needs.\nSimple and reliable.",
     "amazon": amazon_search_link("TP-Link Archer C5"),
     "flipkart": flipkart_search_link("TP-Link Archer C5")},
    {"name":"D-Link M32 (mesh)",
     "description":"AX3200 mesh kit for whole-home coverage.\nFast and stable for modern broadband.\nGood value among AX mesh kits.",
     "amazon": amazon_search_link("D-Link M32"),
     "flipkart": flipkart_search_link("D-Link M32")},
    {"name":"ASUS Blue Cave",
     "description":"Stylish AC2600 router with strong features.\nUnique design with decent throughput.\nGreat for design-conscious homes.",
     "amazon": amazon_search_link("ASUS Blue Cave"),
     "flipkart": flipkart_search_link("ASUS Blue Cave")},
    {"name":"TP-Link Archer C2",
     "description":"Entry-level AC750 router for basic needs.\nCompact and affordable.\nWorks well for small apartments.",
     "amazon": amazon_search_link("TP-Link Archer C2"),
     "flipkart": flipkart_search_link("TP-Link Archer C2")},
    {"name":"Netgear Nighthawk RAXE500 (alt)",
     "description":"Premium Wi-Fi 6E capable router for highest performance.\nStrong multiband throughput and features.\nIdeal for advanced home networks.",
     "amazon": amazon_search_link("Netgear RAXE500"),
     "flipkart": flipkart_search_link("Netgear RAXE500")},
    {"name":"Linksys EA6350",
     "description":"AC1200 dual-band router with reliable performance.\nGood for streaming and home offices.\nEasy setup and secure firmware.",
     "amazon": amazon_search_link("Linksys EA6350"),
     "flipkart": flipkart_search_link("Linksys EA6350")},
    {"name":"TP-Link Archer AX90 Mini",
     "description":"Compact tri-band AX router variant.\nGood for space-constrained setups.\nBalanced performance for many devices.",
     "amazon": amazon_search_link("TP-Link Archer AX90"),
     "flipkart": flipkart_search_link("TP-Link Archer AX90")},
    {"name":"ASUS RT-AX56U",
     "description":"AX1800 entry-level AX router.\nGood value and stable firmware.\nPerfect for upgrading to Wi-Fi 6.",
     "amazon": amazon_search_link("ASUS RT-AX56U"),
     "flipkart": flipkart_search_link("ASUS RT-AX56U")},
    {"name":"TP-Link Archer AXE200 (Wi-Fi 7)",
     "description":"Early Wi-Fi 7 compatible model.\nPrepared for future device ecosystems.\nHigh theoretical bandwidth.",
     "amazon": amazon_search_link("TP-Link Archer AXE200"),
     "flipkart": flipkart_search_link("TP-Link Archer AXE200")},
    {"name":"Netgear Nighthawk R7000P",
     "description":"Enhanced R7000 variant with better throughput.\nGood for medium-large homes.\nStable firmware and feature set.",
     "amazon": amazon_search_link("Netgear R7000P"),
     "flipkart": flipkart_search_link("Netgear R7000P")},
    {"name":"Linksys MR7350",
     "description":"AX1800 mesh-capable router with easy setup.\nCompact design, decent range.\nGreat for single-floor apartments.",
     "amazon": amazon_search_link("Linksys MR7350"),
     "flipkart": flipkart_search_link("Linksys MR7350")},
    {"name":"TP-Link Archer C80",
     "description":"AC1900 router with strong 5GHz performance.\nGood streaming and gaming on mid-range budgets.\nSolid hardware for the price.",
     "amazon": amazon_search_link("TP-Link Archer C80"),
     "flipkart": flipkart_search_link("TP-Link Archer C80")},
    {"name":"ASUS RT-AC5300",
     "description":"Tri-band AC5300 for heavy multi-device homes.\nRich feature set and USB sharing.\nGood for advanced setups.",
     "amazon": amazon_search_link("ASUS RT-AC5300"),
     "flipkart": flipkart_search_link("ASUS RT-AC5300")},
    {"name":"TP-Link TL-WR841N",
     "description":"Classic N300 model for legacy devices.\nUltra-affordable and compact.\nGood for simple Wi-Fi hotspots.",
     "amazon": amazon_search_link("TP-Link TL-WR841N"),
     "flipkart": flipkart_search_link("TP-Link TL-WR841N")},
    {"name":"Netgear Nighthawk XR1000",
     "description":"Gaming-focused AX router with DumaOS.\nOptimized for low-latency and routing.\nGood for competitive gamers.",
     "amazon": amazon_search_link("Netgear Nighthawk XR1000"),
     "flipkart": flipkart_search_link("Netgear Nighthawk XR1000")},
    {"name":"Linksys EA5400",
     "description":"AC1200 dual-band router with stable performance.\nGood for small family usage.\nSimple dashboard and sharing.",
     "amazon": amazon_search_link("Linksys EA5400"),
     "flipkart": flipkart_search_link("Linksys EA5400")},
    {"name":"Tenda AC1200 (Basic)",
     "description":"Generic AC1200 router for budget buyers.\nReliable performance for everyday use.\nEasy to setup with app.",
     "amazon": amazon_search_link("Tenda AC1200 router"),
     "flipkart": flipkart_search_link("Tenda AC1200")},
    {"name":"ASUS RT-AX92U",
     "description":"Tri-band AX mesh capable router.\nGood AiMesh integration and range.\nBalanced for medium-large homes.",
     "amazon": amazon_search_link("ASUS RT-AX92U"),
     "flipkart": flipkart_search_link("ASUS RT-AX92U")},
    {"name":"TP-Link Archer A9",
     "description":"AC1900 router with smart features.\nGood throughput for streaming and gaming.\nUser-friendly app and setup.",
     "amazon": amazon_search_link("TP-Link Archer A9"),
     "flipkart": flipkart_search_link("TP-Link Archer A9")},
]

# ---------- persistent storage ----------
USER_FILE = "users.json"
if os.path.exists(USER_FILE):
    try:
        with open(USER_FILE, "r") as f:
            st.session_state.setdefault("users_db", json.load(f))
    except Exception:
        st.session_state.setdefault("users_db", {})
else:
    st.session_state.setdefault("users_db", {})
st.session_state.setdefault("user", None)

# ---------- auth UI ----------
def signup_page():
    st.title("Create an Account")
    username = st.text_input("Choose a Username", key="su_user")
    password = st.text_input("Choose a Password", type="password", key="su_pass")
    if st.button("Sign Up"):
        if username in st.session_state["users_db"]:
            st.error("Username exists")
        else:
            st.session_state["users_db"][username] = {"password": password, "favorites": []}
            with open(USER_FILE, "w") as f:
                json.dump(st.session_state["users_db"], f, indent=2)
            st.session_state["user"] = username
            st.success("Account created and logged in")
            st.rerun()

def login_page():
    st.title("Login")
    username = st.text_input("Username", key="li_user")
    password = st.text_input("Password", type="password", key="li_pass")
    if st.button("Login"):
        if username in st.session_state["users_db"] and st.session_state["users_db"][username]["password"] == password:
            st.session_state["user"] = username
            st.success("Login successful")
            st.rerun()
        else:
            st.error("Invalid credentials")

# ---------- favorites and product listing ----------
def favorites_page():
    st.title("Favorites")
    user = st.session_state["user"]
    if not user:
        st.info("Login to see favorites")
        return
    favs = st.session_state["users_db"][user].get("favorites", [])
    if not favs:
        st.info("No favorites yet")
        return
    for idx, p in enumerate(favs):
        st.subheader(p["name"])
        st.markdown("  \n".join([f"• {line}" for line in p["description"].split("\n")]))
        c1, c2, c3 = st.columns(3)
        with c1:
            store_button(p.get("amazon", amazon_search_link(p["name"])), "Buy on Amazon")
        with c2:
            store_button(p.get("flipkart", flipkart_search_link(p["name"])), "Buy on Flipkart")
        with c3:
            if st.button("Remove", key=f"rm_{idx}"):
                st.session_state["users_db"][user]["favorites"].pop(idx)
                with open(USER_FILE, "w") as f:
                    json.dump(st.session_state["users_db"], f, indent=2)
                st.success("Removed")
                st.rerun()

def product_listing():
    st.title("Available Wi-Fi Routers")
    user = st.session_state["user"]
    q = st.text_input("Search routers by name (optional)")
    filtered = products
    if q:
        ql = q.lower()
        filtered = [p for p in products if ql in p["name"].lower() or ql in p["description"].lower()]
    for i in range(0, len(filtered), 2):
        cols = st.columns(2)
        for j, col in enumerate(cols):
            if i+j < len(filtered):
                p = filtered[i+j]
                with col:
                    st.subheader(p["name"])
                    st.markdown("  \n".join([f"• {line}" for line in p["description"].split("\n")]))
                    b1, b2, b3 = st.columns([1,1,1])
                    with b1:
                        store_button(p.get("amazon", amazon_search_link(p["name"])), "Buy on Amazon")
                    with b2:
                        store_button(p.get("flipkart", flipkart_search_link(p["name"])), "Buy on Flipkart")
                    with b3:
                        if st.button("❤ Save to Favorites", key=f"fav_{i+j}"):
                            if p not in st.session_state["users_db"][user]["favorites"]:
                                st.session_state["users_db"][user]["favorites"].append(p)
                                with open(USER_FILE, "w") as f:
                                    json.dump(st.session_state["users_db"], f)
                                st.success(f"Added {p['name']} to favorites!")

# ---------- main ----------
def main():
    st.sidebar.title("Navigation")
    if not st.session_state["user"]:
        page = st.sidebar.radio("Go to", ["Login", "Sign Up"])
        if page == "Login":
            login_page()
        else:
            signup_page()
    else:
        choice = st.sidebar.radio("Go to", ["Products", "Favorites", "Logout"])
        if choice == "Products":
            product_listing()
        elif choice == "Favorites":
            favorites_page()
        else:
            st.session_state["user"] = None
            st.success("Logged out")
            st.rerun()

if __name__ == "__main__":
    main()
