# Week26
1.Будет отрисован компонент <Route path="/users" element={<Users />} />
Потому что он является наиболее подходящим путем. Изменение порядка роутов не влияет на отрисовку подходящего пути.

2.На экране появится сообщение "Моя личная страница".

3.Вторым параметром map() принимает индекс(index) элемента в текущей итерации.

4.Вывести товары, цена которых не превышает заданную:
shoes.filter((elem) => elem.price < priceLimit)

5.import React, { Fragment } from "react";
import { BrowserRouter as Router, Route, Link, Switch } from "react-router-dom";
import { useHistory, useParams } from "react-router";
// About Page
const About = () => {
  const hist = useHistory();
  return (
    <div>
      <h1>About</h1>
      <button onClick={() => hist.goBack()}>Go Back</button>
      <LoremText />
    </div>
  );
};
const Shop = () => {
  const params = useParams();
  const current = params.id;
  const next = Number(current) + 1;
  const hist = useHistory();
  return (
    <div>
      <h1>Shop</h1>
      <p>You requested item with ID: {current}</p>
      <button onClick={() => hist.goBack()}>Go Back</button>
      <button onClick={() => hist.push(/shop/${next})}>Next product</button>
    </div>
  );
};
export default function App() {
  return (
    <Router>
      <main>
        <nav>
          <ul>
            <li><Link to="/">Home</Link></li>
            <li><Link to="/about">About</Link></li>
            <li><Link to="/shop/1">Shop</Link></li>
          </ul>
        </nav>
        <Switch>
          <Route exact path="/">
            <Home />
          </Route>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/shop/:id">
            <Shop />
          </Route>
        </Switch>
      </main>
    </Router>
  );
}
// Home Page
const Home = () => (
  <Fragment>
    <h1>Home</h1>
    <LoremText />
  </Fragment>
);
const LoremText = () => (
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
)

6.
- element принимает функцию, которая должна вернуть элемент React. Она будет вызвана, когда удовлетворится сопоставление в path.
- props children будет всегда отображаться независимо от того, сопоставляется ли path или нет.

7.Свойство exact проводит строгую проверку в path. Например, отрисуется только строгое сравнение '/about' или '/about/', но не '/about/chapter1'.

8.useMatch сопоставляет шаблон пути маршрута с именем URL-адреса и возвращает информацию о совпадении. Это полезно, когда нужно вручную запустить алгоритм сопоставления маршрутизатора, чтобы определить, соответствует ли путь маршрута или нет. Он возвращает значение null, если шаблон не соответствует заданному пути.

Местоположение — это объект, который представляет местоположение URL. Он основан на объекте браузера window.location. Хук useLocation возвращает объект текущего местоположения. В переменную location мы сохраняем местоположение, которое генерируется хуком useLocation. Внутри хука useEffect мы будем выводить текущее местоположение при каждом изменении параметра location.

useNavigate возвращает функцию, которую можно использовать для программной навигации.
Хук useNavigate может принимать:
Либо значение To с необязательным вторым аргументом { replace, state }, как это работает и в <Link to>
Либо дельта-число, чтобы войти в стек истории. Например, навигация (-1) по своей сути аналогична нажатию кнопки «Назад».

9.import React, { useEffect } from 'react';
import { Outlet, useLocation, useNavigate } from 'react-router-dom';

const MainPage = () => {
  const location = useLocation();
  const navigate = useNavigate();

  useEffect(() => {
    console.log('Current location is ', location);
  }, [location]);

  return (
    <>
      <nav>
        <ul>
          <li>
            <button onClick={() => navigate('one', { replace: false })}>
              Page One
            </button>
          </li>
          <li>
            <button onClick={() => navigate('two', { replace: false })}>
              Page Two
            </button>
          </li>
        </ul>
      </nav>
      <hr />
      <Outlet />
    </>
  )
};