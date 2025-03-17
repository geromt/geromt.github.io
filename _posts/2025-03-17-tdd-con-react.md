---
layout: post
title:  "TDD con React y Vite"
date:   2025-03-17 17:00:00 -0600
categories: React Vite
---

# TDD con React y Vite

## TDD

TDD (Test-Driven Development) es una técnica para desarrollar software en la que el desarrollo es guiado por las pruebas. Los desarrolladores escriben las pruebas y luego escriben el código.

El TDD es un proceso iterativo que consiste de 3 pasos:
- Escribimos un test que falla
- Escribimos el código mínimo necesario para que pase el test
- Refactorizamos los test y el código, si es necesario

### Leyes del TDD

- No escribir código de producción hasta que hayas escrito un test que falle
- No escribir más un test que falle
- No escribir más código del necesario para que pase el test

## Qué librerías instalar para Vite y React

Al trabajar con `Vite` al principio intenté utilizar jest, pero nunca logra configurarlo, por eso mejor utilizo `vitest`

```
npm install -D vitest
```

En el `package.json` agregar los scripts 

```
"scripts": {
  "test": "vitest",
  "coverage": "vitest run --coverage"
}
```

Para hacer test con React tenemos que instalar 

```
npm install @testing-library/react -D
npm install @testing-library/user-event -D
npm install happy-dom -D
```

`happy-dom` es una alternativa a `js-dom`, pero más rápido

### Installar React en Vite

`Vite` puede configurar un proyecto de React seleccionándolo, pero si comenzaste con un proyecto de `javascript` vanilla puedes configurarlo con 

```
npm install react react-dom -E
npm install @vitejs/plugin-react -D
```

Crear un `vite.config.js` con el siguiente código

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'happy-dom'
  }
})
```


### Ejemplo de test con vitest

```javascript
describe("Component", () => {
  afterEach(cleanup)

  it("Should test something", () => {
    render(<Component />)
    screen.getByText('text')
    screen.getByRole('role')
  })

  it("Should render the correct symbol in the square", () => {
    const board = ['X', null, 'O', null, 'X', null, 'O', null, 'X']
    const updateBoard = vi.fn()
    render(<Board board={board} updateBoard={updateBoard}/>)
    const squares = screen.getAllByRole('square')
    for (let i = 0; i < board.length; i++) {
      expect(squares[i].textContent).toBe(board[i] ?? '')
    }
  })

  it("Should render the winner when there is a winner", async () => {
    render(<TicTacToe />)
    const boardBoxes = screen.getAllByRole("square")
    await userEvent.click(boardBoxes[0])
    await userEvent.click(boardBoxes[3])
    await userEvent.click(boardBoxes[1])
    await userEvent.click(boardBoxes[4])
    await userEvent.click(boardBoxes[2])
    screen.getByText("Winner:")
  })
})
```