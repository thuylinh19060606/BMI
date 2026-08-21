import matplotlib.pyplot as plt
import streamlit as st


st.set_page_config(
    page_title="á»¨ng dá»¥ng tÃ­nh chá»‰ sá»‘ BMI",
    page_icon="âš–ï¸",
    layout="wide",
)


def tinh_bmi(can_nang: float, chieu_cao: float):
    """TÃ­nh BMI, khoáº£ng cÃ¢n náº·ng lÃ½ tÆ°á»Ÿng vÃ  thÃ´ng tin phÃ¢n loáº¡i."""
    chieu_cao_m = chieu_cao / 100
    bmi = can_nang / (chieu_cao_m**2)

    can_nang_toi_thieu = 18.5 * (chieu_cao_m**2)
    can_nang_toi_da = 24.9 * (chieu_cao_m**2)

    if bmi < 18.5:
        phan_loai = "Thiáº¿u cÃ¢n"
        mau_nhan = "#f59e0b"
        mau_nen = "#fff7ed"
    elif bmi < 25:
        phan_loai = "BÃ¬nh thÆ°á»ng"
        mau_nhan = "#16a34a"
        mau_nen = "#f0fdf4"
    elif bmi < 30:
        phan_loai = "Thá»«a cÃ¢n"
        mau_nhan = "#f59e0b"
        mau_nen = "#fff7ed"
    else:
        phan_loai = "BÃ©o phÃ¬"
        mau_nhan = "#dc2626"
        mau_nen = "#fef2f2"

    return {
        "bmi": bmi,
        "bmi_lam_tron": round(bmi, 1),
        "can_nang_toi_thieu": can_nang_toi_thieu,
        "can_nang_toi_da": can_nang_toi_da,
        "phan_loai": phan_loai,
        "mau_nhan": mau_nhan,
        "mau_nen": mau_nen,
    }


def tao_bieu_do_bmi(bmi: float, bmi_lam_tron: float):
    """Táº¡o biá»ƒu Ä‘á»“ ngang thá»ƒ hiá»‡n vá»‹ trÃ­ BMI trÃªn thang 15â€“40."""
    fig, ax = plt.subplots(figsize=(11, 2.7))

    cac_vung = [
        (15, 3.5, "#fbbf24", "Thiáº¿u cÃ¢n", 16.75),
        (18.5, 6.5, "#22c55e", "BÃ¬nh thÆ°á»ng", 21.75),
        (25, 5, "#fb923c", "Thá»«a cÃ¢n", 27.5),
        (30, 10, "#ef4444", "BÃ©o phÃ¬", 35),
    ]

    for diem_bat_dau, do_rong, mau, ten_vung, vi_tri_chu in cac_vung:
        ax.barh(
            0,
            do_rong,
            left=diem_bat_dau,
            height=0.5,
            color=mau,
        )
        ax.text(
            vi_tri_chu,
            0,
            ten_vung,
            ha="center",
            va="center",
            fontsize=9,
            fontweight="bold",
        )

    # Náº¿u BMI náº±m ngoÃ i thang hiá»ƒn thá»‹, Ä‘iá»ƒm Ä‘Ã¡nh dáº¥u Ä‘Æ°á»£c ghim vÃ o mÃ©p biá»ƒu Ä‘á»“.
    vi_tri_danh_dau = min(max(bmi, 15), 40)
    ax.axvline(
        vi_tri_danh_dau,
        color="#111827",
        linewidth=3,
        linestyle="--",
    )
    ax.scatter(vi_tri_danh_dau, 0, color="#111827", s=90, zorder=5)
    ax.text(
        vi_tri_danh_dau,
        0.42,
        f"BMI cá»§a báº¡n: {bmi_lam_tron:.1f}",
        ha="center",
        va="bottom",
        fontsize=11,
        fontweight="bold",
        color="#111827",
    )

    ax.set_xlim(15, 40)
    ax.set_ylim(-0.55, 0.75)
    ax.set_yticks([])
    ax.set_xticks([15, 18.5, 25, 30, 35, 40])
    ax.set_xlabel("Thang chá»‰ sá»‘ BMI")
    ax.set_title("Vá»‹ trÃ­ BMI cá»§a báº¡n", fontweight="bold")

    for vi_tri in ["top", "left", "right"]:
        ax.spines[vi_tri].set_visible(False)

    fig.tight_layout()
    return fig


st.markdown(
    """
    <style>
        .stApp {
            background: linear-gradient(135deg, #f0f9ff, #f8fafc);
        }
        .block-container {
            max-width: 1050px;
            padding-top: 2rem;
            padding-bottom: 2rem;
        }
        .tieu-de {
            text-align: center;
            color: #0f172a;
            margin-bottom: 0.25rem;
        }
        .mo-ta {
            text-align: center;
            color: #475569;
            font-size: 1rem;
            margin-bottom: 1.5rem;
        }
        .the-ket-qua {
            background: white;
            border: 1px solid #e2e8f0;
            border-radius: 16px;
            padding: 1rem 1.1rem;
            box-shadow: 0 8px 25px rgba(15, 23, 42, 0.06);
            margin-bottom: 0.75rem;
        }
        .nhan-nho {
            color: #64748b;
            font-size: 0.9rem;
            margin-bottom: 0.2rem;
        }
        .gia-tri-lon {
            color: #0f172a;
            font-size: 2rem;
            font-weight: 700;
            line-height: 1.25;
        }
        .gia-tri-can-nang {
            color: #0f172a;
            font-size: 1.35rem;
            font-weight: 650;
            line-height: 1.5;
        }
        .mien-tru {
            text-align: center;
            color: #64748b;
            font-size: 0.82rem;
            margin-top: 1.5rem;
            padding: 0.8rem;
            border-top: 1px solid #cbd5e1;
        }
        div[data-testid="stFormSubmitButton"] > button {
            width: 100%;
            color: white;
            font-weight: 700;
            background: linear-gradient(90deg, #0284c7, #2563eb);
            border: none;
        }
    </style>
    """,
    unsafe_allow_html=True,
)

st.markdown(
    '<h1 class="tieu-de">âš–ï¸ á»¨ng dá»¥ng tÃ­nh chá»‰ sá»‘ BMI</h1>',
    unsafe_allow_html=True,
)
st.markdown(
    """
    <p class="mo-ta">
        Äiá»u chá»‰nh cÃ¢n náº·ng vÃ  chiá»u cao Ä‘á»ƒ tÃ­nh BMI, xem phÃ¢n loáº¡i
        vÃ  khoáº£ng cÃ¢n náº·ng lÃ½ tÆ°á»Ÿng cá»§a báº¡n.
    </p>
    """,
    unsafe_allow_html=True,
)

cot_nhap, cot_ket_qua = st.columns([1, 1], gap="large")

with cot_nhap:
    st.subheader("ThÃ´ng tin cá»§a báº¡n")
    with st.form("bieu_mau_bmi"):
        can_nang = st.slider(
            "CÃ¢n náº·ng (kg)",
            min_value=30,
            max_value=200,
            value=60,
            step=1,
        )
        chieu_cao = st.slider(
            "Chiá»u cao (cm)",
            min_value=100,
            max_value=220,
            value=165,
            step=1,
        )
        st.form_submit_button("TÃ­nh chá»‰ sá»‘ BMI", type="primary")

ket_qua = tinh_bmi(can_nang, chieu_cao)

with cot_ket_qua:
    st.subheader("Káº¿t quáº£")
    st.markdown(
        f"""
        <div class="the-ket-qua">
            <div class="nhan-nho">Chá»‰ sá»‘ BMI</div>
            <div class="gia-tri-lon">{ket_qua['bmi_lam_tron']:.1f}</div>
        </div>
        <div class="the-ket-qua">
            <div class="nhan-nho">Khoáº£ng cÃ¢n náº·ng lÃ½ tÆ°á»Ÿng</div>
            <div class="gia-tri-can-nang">
                {ket_qua['can_nang_toi_thieu']:.1f} kg â€“
                {ket_qua['can_nang_toi_da']:.1f} kg
            </div>
        </div>
        <div style="
            background-color: {ket_qua['mau_nen']};
            border: 2px solid {ket_qua['mau_nhan']};
            border-radius: 12px;
            padding: 14px;
            text-align: center;
            color: {ket_qua['mau_nhan']};
            font-size: 22px;
            font-weight: bold;
        ">
            {ket_qua['phan_loai']}
        </div>
        """,
        unsafe_allow_html=True,
    )

st.subheader("Biá»ƒu Ä‘á»“ phÃ¢n loáº¡i BMI")
bieu_do = tao_bieu_do_bmi(ket_qua["bmi"], ket_qua["bmi_lam_tron"])
st.pyplot(bieu_do, use_container_width=True)
plt.close(bieu_do)

st.markdown(
    """
    <div class="mien-tru">
        <strong>Miá»…n trá»« trÃ¡ch nhiá»‡m:</strong>
        Káº¿t quáº£ BMI vÃ  khoáº£ng cÃ¢n náº·ng lÃ½ tÆ°á»Ÿng trong á»©ng dá»¥ng nÃ y chá»‰ mang
        tÃ­nh cháº¥t tham kháº£o, khÃ´ng thay tháº¿ cho viá»‡c thÄƒm khÃ¡m, cháº©n Ä‘oÃ¡n
        hoáº·c tÆ° váº¥n cá»§a bÃ¡c sÄ© vÃ  chuyÃªn gia y táº¿.
    </div>
    """,
    unsafe_allow_html=True,
)
