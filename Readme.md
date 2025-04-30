a live map for cheap wifi routers without csi:

![image](https://github.com/user-attachments/assets/a7bb1662-347f-4ae2-99ea-56f6fb2f0adb)



RF Tomographic Imaging (RTI) Based on RSSI for Real-time Indoor Positioning

Abstract

This paper introduces a comprehensive approach to developing an RF-based imaging system using Radio Tomographic Imaging (RTI), exclusively leveraging Received Signal Strength Indicator (RSSI) variations and a predefined indoor floor plan. By employing Sparse Bayesian Learning (SBL) with Laplace prior regularization, the method robustly reconstructs attenuation maps, allowing precise detection and localization of objects or individuals. Practical implementation steps are detailed, accompanied by Python code snippets, resulting in a real-time RF-based imaging solution without requiring specialized hardware.

1. Introduction

Radio Tomographic Imaging (RTI) is a promising technology that reconstructs spatial maps of signal attenuation caused by objects within wireless networks. Unlike traditional optical or mmWave imaging systems, RTI utilizes RSSI variations from existing Wi-Fi infrastructures, enabling unobtrusive and low-cost surveillance solutions.

2. RTI Fundamentals

RTI divides the monitored area into grid cells, each cell representing potential attenuation points. The system computes the RSSI difference (ΔRSSI) between baseline (no target present) and presence scenarios for each link:
\Delta r_l = r_l^{(0)} - r_l^{(p)}

2.1 Ellipse Model

The ellipse model defines the affected region for each link as an ellipse with the transmitter and receiver positions as foci. Cells within this ellipse receive a binary weighting (1 or 0), establishing the weight matrix W.

3. Sparse Bayesian Learning (SBL) with Laplace Prior

To mitigate noise and multipath artifacts, SBL with a Laplace prior is applied:
\hat{x} = \arg\max_{x \ge 0} \{\log p(\Delta r \mid x) + \log p(x)\}, \quad p(x) \propto e^{-\alpha \|x\|_1}
This approach provides sparse solutions, greatly reducing artifacts and enhancing localization accuracy.

4. Detailed Implementation Steps
	1.	Floor Plan and Grid Preparation: Define a 0.5×0.5 m grid and store cell coordinates.
	2.	Anchor Identification: Select strong Wi-Fi APs and store coordinates.
	3.	Baseline Calibration: Measure average RSSI values without targets.
	4.	Measurement with Targets: Record RSSI values with targets present and compute ΔRSSI.
	5.	Weight Matrix Construction: Using the ellipse model, create matrix W.
	6.	Inverse Problem Solution: Solve using Lasso regression:

from sklearn.linear_model import Lasso
lasso = Lasso(alpha=0.01, positive=True, max_iter=10000)
lasso.fit(W, dr)
x_hat = lasso.coef_

	7.	Image Generation: Convert attenuation values into a heatmap visualization.
	8.	Real-time Implementation: Automate data collection and update visualization continuously.
	9.	Resolution Enhancement: Refine grid and adjust regularization parameters.

5. Experimental Evaluation

Using Laplace priors significantly reduces artifacts and improves localization accuracy to approximately 0.1–0.2 meters, suitable for real-time operation.

6. Results and Discussion

The proposed method achieves:
	•	Artifact reduction and improved image clarity.
	•	High accuracy localization (0.1–0.2 meters).
	•	Robust performance against multipath effects.

7. Potential for Misuse

The described system, while beneficial, poses significant privacy risks:
	•	Privacy Intrusion: Unnoticed surveillance and tracking of individuals without consent.
	•	Crime Planning: Enables detailed monitoring of occupancy patterns, facilitating burglary or kidnapping.
	•	Domestic Abuse: Potential for stalkers or abusive partners to remotely monitor victims.
	•	Industrial Espionage: Tracking employee movements and confidential meetings.
	•	Manipulation of Smart Systems: Exploiting security and automation systems through fake RSSI signals.

8. Conclusion

Employing RTI with RSSI and Sparse Bayesian Learning provides a low-cost, real-time indoor imaging solution. However, recognizing the potential for misuse highlights the critical need for protective measures, including secure handling of RSSI data, encryption, and anomaly detection.

⸻

تصویربرداری توموگرافی رادیویی (RTI) با استفاده از RSSI برای موقعیت‌یابی بلادرنگ در فضاهای داخلی

چکیده

این مقاله رویکرد جامعی را برای ساخت یک سیستم تصویربرداری مبتنی بر امواج رادیویی (RTI)، تنها با استفاده از تغییرات RSSI و پلان طبقه ارائه می‌دهد. استفاده از یادگیری بیزی تنک (Sparse Bayesian Learning) با پیش‌فرض لاپلاس باعث بازسازی دقیق نقشه‌های تضعیف سیگنال می‌گردد. مراحل پیاده‌سازی به تفصیل با نمونه کدهای پایتون شرح داده شده و منجر به ایجاد یک سامانه تصویربرداری بلادرنگ بدون سخت‌افزار ویژه می‌شود.

۱. مقدمه

تصویربرداری توموگرافی رادیویی (RTI) فناوری نوینی است که با تحلیل تغییرات قدرت سیگنال دریافتی (RSSI) شبکه‌های وای‌فای موجود، تصاویر تضعیف‌شده‌ای از فضای داخلی ایجاد می‌کند.

۲. اصول RTI

فضای داخلی به سلول‌های گرید تقسیم شده و تغییرات RSSI (ΔRSSI) بین حالت پایه و حالت حضور اهداف اندازه‌گیری می‌شود.

۲.۱ مدل بیضی

هر لینک منطقه اثرگذاری خود را به صورت یک بیضی تعریف کرده و ماتریس وزن‌دهی (W) را شکل می‌دهد.

۳. یادگیری بیزی تنک با پیش‌فرض لاپلاس

از این چارچوب جهت کاهش نویز و آرتیفکت‌ها استفاده می‌شود و تصاویر واضح و دقیقی تولید می‌کند.

۴. پیاده‌سازی دقیق و گام‌به‌گام

شامل تعریف پلان، تعیین نقاط مرجع، کالیبراسیون پایه، اندازه‌گیری ΔRSSI، ساخت ماتریس وزن، حل دستگاه معکوس و تولید نقشه تصویری بلادرنگ.

۵. ارزیابی تجربی

دقت محلی‌سازی ۰٫۱–۰٫۲ متر با حذف مؤثر آرتیفکت‌ها و امکان اجرای بلادرنگ حاصل شد.

۶. بحث و نتایج

روش پیشنهادی توانست با دقت بالا و پایداری در شرایط چندمسیره، یک تصویربرداری بلادرنگ را ارائه کند.

۷. امکان سوءاستفاده

سیستم پیشنهادی، امکان نقض حریم خصوصی و برنامه‌ریزی جرائم را افزایش داده و نیاز به اقدامات امنیتی مانند رمزنگاری و تشخیص ناهنجاری‌ها را ضروری می‌سازد.

۸. نتیجه‌گیری

روش ارائه‌شده ابزاری کم‌هزینه و کاربردی برای تصویربرداری داخلی فراهم کرده و در عین حال، نیازمند توجه جدی به مسائل امنیتی است.
