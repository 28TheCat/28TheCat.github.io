---
title: 关于我
---

<style>
  .about-profile {
    max-width: 720px;
    margin: 0 auto;
    color: var(--post-text-color);
  }

  .about-profile__intro {
    padding-bottom: 1.35rem;
    border-bottom: 1px solid rgba(127, 127, 127, 0.18);
  }

  .about-profile__hello {
    margin: 0 0 0.45rem;
    color: var(--sec-text-color);
    font-weight: 600;
  }

  .about-profile__name {
    margin: 0;
    color: var(--post-heading-color);
    font-size: 2rem;
    line-height: 1.25;
    font-weight: 700;
  }

  .about-profile__desc {
    margin: 0.65rem 0 0;
    color: var(--sec-text-color);
  }

  .about-profile__section {
    padding: 1.3rem 0;
    border-bottom: 1px solid rgba(127, 127, 127, 0.14);
  }

  .about-profile__section-title {
    margin: 0 0 0.8rem;
    color: var(--post-heading-color);
    font-size: 1.25rem;
    line-height: 1.35;
  }

  .about-profile__identity {
    margin: 0;
    font-weight: 600;
  }

  .about-profile__education {
    display: grid;
    grid-template-columns: 8.5rem minmax(0, 1fr);
    gap: 0.25rem 1rem;
    align-items: start;
  }

  .about-profile__time {
    grid-row: 1 / span 2;
    margin: 0;
    color: var(--sec-text-color);
    font-weight: 600;
  }

  .about-profile__school {
    margin: 0;
    color: var(--post-heading-color);
    font-weight: 700;
  }

  .about-profile__major {
    margin: 0;
    color: var(--sec-text-color);
  }

  .about-profile__contact-text {
    margin: 0 0 0.8rem;
  }

  .about-profile .contact-icons {
    display: flex;
    gap: 0.75rem;
    margin: 0;
  }

  .about-profile .contact-icons a {
    display: inline-flex;
    width: 2.4rem;
    height: 2.4rem;
    align-items: center;
    justify-content: center;
    border: 1px solid rgba(127, 127, 127, 0.2);
    border-radius: 999px;
    color: var(--post-text-color);
    background: rgba(127, 127, 127, 0.08);
    text-decoration: none;
    transition: color 0.18s ease, border-color 0.18s ease, transform 0.18s ease;
  }

  .about-profile .contact-icons a:hover {
    color: var(--link-hover-color);
    border-color: var(--link-hover-color);
    transform: translateY(-2px);
  }

  .about-profile .contact-icons .iconfont {
    font-size: 1.25rem;
  }

  @media (max-width: 575px) {
    .about-profile__name {
      font-size: 1.65rem;
    }

    .about-profile__education {
      display: block;
    }

    .about-profile__time {
      margin-bottom: 0.35rem;
    }
  }
</style>

<div class="about-profile">
  <section class="about-profile__intro">
    <p class="about-profile__hello">你好呀！</p>
    <h2 class="about-profile__name">28theCat</h2>
    <p class="about-profile__desc">普通路过计算机专业的本科生。</p>
  </section>

  <section class="about-profile__section">
    <h2 class="about-profile__section-title">基本信息</h2>
    <p class="about-profile__identity">28theCat</p>
  </section>

  <section class="about-profile__section">
    <h2 class="about-profile__section-title">教育经历</h2>
    <div class="about-profile__education">
      <p class="about-profile__time">2023.7 - 至今</p>
      <p class="about-profile__school">江西财经大学</p>
      <p class="about-profile__major">计算机与人工智能学院，计算机科学与技术专业，本科</p>
    </div>
  </section>

  <section class="about-profile__section">
    <h2 class="about-profile__section-title">联系方式</h2>
    <p class="about-profile__contact-text">欢迎联系我喵</p>
    <p class="contact-icons">
      <a href="mailto:yating28@qq.com" title="邮箱" aria-label="邮箱">
        <i class="iconfont icon-mail"></i>
      </a>
      <a href="https://github.com/28TheCat" title="GitHub" aria-label="GitHub" target="_blank" rel="noopener">
        <i class="iconfont icon-github-fill"></i>
      </a>
    </p>
  </section>
</div>
