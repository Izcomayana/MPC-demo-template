<template>
  <header>
    <nav class="navbar navbar-expand-lg">
      <div class="container-fluid">
        <a class="mpc-icon" href="#"><img src="../assets/images/mpc-logo.png" alt="mpc"></a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link" aria-current="page" href="#">HOME</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">CLAUSES</a>
            </li>
            <li class="nav-item">
              <a class="nav-link">HELP</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
</script>

<style>
  header {
    background: #002147;
  }

  .mpc-icon {
    width: 2rem;
  }

  .mpc-icon img {
    width: 100%;
  }

  .nav-link {
    cursor: pointer;
    color: white !important;
    font-size: 1.1rem !important;
    width: fit-content !important;
  }

  .nav-link:hover,
  .nav-link:focus,
  .nav-link:active {
    color: rgb(10, 88, 202) !important;
    transition: 250ms ease-in !important;
  }

  .navbar-toggler {
    color: #002147 !important;
    background-color: #FFB45E !important;
    padding: 0 0.5rem !important;
    margin: 0.5rem 0 !important;
  }

  .navbar-toggler:focus {
    box-shadow: none !important;
  }

  .navbar-toggler-icon {
    width: 1.3em !important;
    height: 1.3em !important;
  }

  .navbar-collapse {
    flex-grow: 0 !important;
  }
</style>