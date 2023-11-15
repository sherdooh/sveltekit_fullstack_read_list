<script>
  let myLib = ["Head First Javascript"];
  let currBook = "";
  let error = false;

  function addBook() {
    error = false;
    if (!currBook) {
      error = true;
      return;
    }
    myLib = [...myLib, currBook];
    currBook = "";
  }

function editBook(index) {
  let newMyLib = myLib.filter((val, i) => {
    return i !== index;
  });
  currBook = myLib[index]
  myLib = newMyLib
}

function removeBook(index) {
  let newMyLib = myLib.filter((val, i) => {
    return i !== index;
  });
  myLib = newMyLib

}

</script>

<div class="mainContainer">
  <div class="headerContainer">
    <h1>My Library</h1>
    
    <div class="headerBtns">
      <button class="fa-solid fa-floppy-disk">Save</button>

      <button class="fa-solid fa-right-from-bracket">Logout</button>

    </div>
  </div>
  <main>
    {#if myLib.lenght === 0}

    <p>
      Your book list is empty!!
    </p>
      
    {/if}
    {#each myLib as book, index}
      <div class="book">
       <p>
        {index + 1}, {book}
       </p>
       <div class="actions">
        <button on:click={() => {editBook(index);
        }}
        on:keydown={() => {}}
        ><i class="fa-solid fa-pen-nib"></i></button>
        <button on:click={() => {removeBook(index);
        }}
        on:keydown={() => {}}><i class="fa-solid fa-trash-can"></i></button>

       </div>
      </div>
    {/each}
  </main>
  <div class={"toRead" + (error ? "errorBorder" : "")}>
    <input bind:value={currBook} type="text" placeholder="Enter Book" />
    <button on:click={addBook}>ADD</button>
  </div>
</div>

<style>
  .mainContainer {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    gap: 24px;
    padding: 24px;
    width: 100%;
    max-width: 1000px;
    margin: 0 auto;
  }

  .headerContainer {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .headerBtns {
    display: flex;
    align-items: center;
    gap: 14px;
    }
  .headerContainer button {
    background: #0892b3;
    padding: 10px 18px;
    border-radius: 4px;
    border: none;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 4px;
    cursor: pointer;
    font-size: 0.7em;
    
  }
  .actions button {
    background: #0892b3;
    padding: 5px 8px;
    border-radius: 4px;
    border: none;
    font-weight: 700;
    align-items: center;
    gap: 4px;
    cursor: pointer;
  }
  .headerContainer button:hover {
    opacity: 0.7;
  }

  main {
    display: flex;
    flex-direction: column;
    gap: 8px;
    flex: 1;
  }
  .book {
    border-left: 1px solid cyan;
    padding: 8px 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .actions{
    display: flex;
    align-items: center;
    gap: 14px;
    font-size: 1.3rem;
  }
  .actions i:hover{
    color: crimson;
  }
  .toRead {
    display: flex;
    align-items: stretch;
    border: 1px solid #0892b3;
    border-radius: 5px;
    overflow: hidden;
  }
  .errorBorder {
    border-color: crimson !important;
  }
  .toRead input {
    background: transparent;
    border: none;
    padding: 14px;
    color: white;
    flex: 1;
  }
  .toRead input:focus {
    outline: none;
  }
  .toRead button {
    padding: 0 14px;
    background: #003c5b;
    border: none;
    color: cyan;
    font-weight: 600;
  }
  .toRead button:hover {
    background: transparent;
    color: white;
  }
</style>
