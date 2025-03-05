<template>
	<section id="profile" class="c-section">
		<div class="section-inner">
			<header class="sectionHeader">
				<h2 class="sectionHeader__ttl">自己紹介</h2>
			</header>
			<div class="sectionBody">
				<dl class="profileTable">
					<div class="profileTable__item">
						<dt class="profileTable__lbl">深水 佳奈<small>（ふかみ かな）</small></dt>
						<dd class="profileTable__des">1995年9月28日生まれ、A型。</dd>
						<dd class="profileTable__des">サウナとラジオが好きです。</dd>
					</div>
				</dl>
			</div>
		</div>
    </section>
</template>

<style scoped>
.profileTable__item + .profileTable__item {
	margin-top: 10px;
}

.profileTable__des {
	margin: 0;
}
</style>